# Ruby on Rails memo

## Foreman hides the logs
Add `STDOUT.sync = true` at the top of your `environments/development.rb`

## Create controller with index page

```bash
rails generate controller ControllerCamelCasedPlural index
```

## add this controller to the routes

Edit `config/routes.rb`

```ruby
MyApp::Application.routes.draw do
  get "controller_camel_cased_plural/index"
  root :to => 'controller_camel_cased_plural#index'
```

## add some initializers in your app
Add a file `config\initializers\yourfile.rb` 
and add the following lines 

```ruby
Rails.application.config.before_initialize do
    YourClass::variable = ENV['environnement_variable']
end
```

Where YourClass is defined like :

```ruby
class YourClass
  class << self
    attr_accessor :variable
  end
end
```

or, better :

```ruby
class YourClass
  cattr_accessor :variable
end
```


## rollback a model 
```
bundle exec rake db:rollback
bundle exec rails destroy model YourModel
```

## Need to return stg if it's been defined and not nil ?

```
return @token unless @token.nil?
```

## need to debug
```
logger.debug "blabla"
```

