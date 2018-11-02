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

```

```ruby


```



