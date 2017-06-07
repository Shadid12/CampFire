# create the user model
rails g scaffold user name:string email:string password:string

# fix CORS
> uncomment this 

```ruby

Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end

```

## For Testing 

```javascript

$(document).ready(function() {
  
  var url = "https://react-like-a-boss-shadid121.c9users.io/users"
  var d = {
    'user':{
      'name':'shadid',
      'email': 'shadid@gmail.com',
      'password': '1234565'
    }
  }
  
  $.ajax({
    type: "POST",
    url: url,
    data: d,
    success: function(res){
      console.log(res);
    }
    
  });
  
});

```

## Validate User
```ruby
class User < ApplicationRecord
    has_secure_password
    before_save { self.email = email.downcase }
    validates :name, presence: true, length: { maximum: 50 }
    VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-]+(\.[a-z]+)*\.[a-z]+\z/i
    validates :email, presence: true, format: { with: VALID_EMAIL_REGEX },
                    uniqueness: { case_sensitive: false }
end
```

