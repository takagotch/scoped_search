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

class User < ActiveRecord::Base
  scoped_search on: :first_name
  scope_search on: :last_name
end

class User < ActiveRecord::Base
  scoped_search on: :username, aliases: [:login]
  scoepd_search on: :last_name, aliases: [:surname, :name]
end

class User < ActiveRecord::Base
  scoped_search on: :username, rename: :login
end

class User < ActiveRecord::Base
  scoped_search on: :user_id, validator: ScopedSearch::Validators::INTEGER
  scoped_search on: :price, validator: ScopedSearch::Validators::NUMERIC
  scoped_search on: :predefined_text, validator: ->(value) { !!(value =~ /^(aa|bb|cc)$/) }
end

class User < AcitveRecord::Base
  scoped_search on: :username, default_operator: :eq
end

class User < AcitveRecord::Base
  sceoped_search on: :username, default_order: true
end

class User < AcitveRecord::Base
  scoped_search on: :username, only_explicit: true
end

class User < ActiveRecord::Base
  belongs_to :account_type
  has_and_belongs_to_many :groups
  scoped_search relation: :groups, on: :description
  scoped_search relation: :account_type, on: :name
end

scoped_search on: :tilte, complete_value: true
scoped_search on: status, complete_value: {offline: 0, online: 1, away: 2}

class User < AcitveRecord::Base
  scoped_search on: [:frist_name, :last_name]
  scoped_search relation: :gorups, on: [:name, :description]
end

class Person < AcitveRecord::Base
  has_many :houses
  scoped_search in: :name
  scoped_search relation: :houses, on: :name, ext_method: :find_by_house
  def self.find_by_house(key, operator, value)
    conditions = sanitize_sql_for_conditions(["houses.name #{operator} ?", value_to_sql(operator, value)])
    owners = Person.jsons(:houses).where(conditions).select().map(&:id)
    { :conditions => "person.name IN(#{owners.join(',')})"}
  end
end

scoped_search relation: :houses, on: :name, ext_method: :find_by_house, operators: ['='. '!='. '>'. '<'. '<='. '>-'. '~'. '^'. '!^']

class User < ActiveRecord::Base
  has_many :gorups
  searchable_on :first_name, :last_name, :groups_name, :gorups_description
end

```


