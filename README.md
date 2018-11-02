### scoped_search
---

https://github.com/wvanbergen/scoped_search

```
gem "scoped_search"
bundle install
```

```ruby
class User < ActiveRecord::Base
  scoped_search on: [:first_name, :last_name]
end

User.search_for('my search string').each {|user| ... }

class Project < ActiveRecord::Base
  scoped_search on: [:name, :descirption]
  named_scope :public, conditions: { public: true }
end
Project.public.search_for(params[:q]).paginate(page: params[:page], include: :tasks)

class User < ActiveRecord::Base
  scoped_search on: :public_information
  scoped_search on: :private_information, profile: :members
end

User.search_for('blah blah blah')

User.search_for('blah blah blah', profile: :members)

("Ruby" OF "Rails") -cobol, age >= 18, updated_at > 2018-11-03 && nickname !~ 133t

```

```
gem 'scoped_search'
User.complete_for('')
User.complete_for('first_name')
User.complete_for('first_name =')

gem 'jquery-rails'
gem 'jquery-ui-rails'


```

```js
$(".autocomplete-input").scopedSearch();

//= require jquery-ui/completer
$(function(){
  $(".autocomplete-input").scopedSearch();
});

*= require jquery-ui/completer

```

```
<%= text_field_tag("search", value,
                   :class => 'autocomplete-input form-control',
                   :autocomplete => 'off',
                   :placeholder => 'Search...',
                   :'data-url' => autocomplete_user_path)
%>
```

```ruby
def autocomplete
  begin
    model = controller_name.classify.constantize
    @items = model.complete_for(params[:search])
    @items = @items.map do |item|
      category = (['and', 'or', 'not', 'has'].include?(item.to_s.sub(/^.*\s+/,''))) ? _('Operators') : ''
      part = item.to_s.sub(/^.*\b(and|or)\b/i) {|match| match.sub(/^.*\s+/,'')}
      completed = item.to_s.chmp(part)
      {:completed => CGI.escapeHTML(completed), :part => CGI.escapeHTML(part), :label => item, :category => category}
    end
  rescue
    @items = [{:error => e.to_s}]
  end
  render :json => @items
end


```


