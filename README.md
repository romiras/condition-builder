# condition-builder
Fork of Duane Johnson's condition-builder to include some additional patches. Read [http://blog.inquirylabs.com/2007/01/04/condition-builder-10-released/](http://web.archive.org/web/20080326215112/http://blog.inquirylabs.com/2007/01/04/condition-builder-10-released/)

This Ruby gem can assist in building complex logic in ActiveRecord queries. Supports Ruby 1.8.7 and Ruby on Rails 2.3.x.

Here are some code samples:
```
  Condition.block { |c|
    c.and "one", 1
    c.and "two", 2
    c.and { |d|
      d.or "three", 3
      d.or "four", 4
    }
  }
```
  # => ["one = ? AND two = ? AND (three = ? OR four = ?)", 1, 2, 3, 4]


```
  Condition.block { |c|
    c.and "user_id", @user_id
    c.and { |d|
      d.or "admin", true
      d.or "joined_at", "<", Date.new(2007, 1, 1)
    } unless @dont_override_user_id
  }
```
