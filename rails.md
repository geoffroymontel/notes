# Ruby on Rails memo

## update Rails
```
gem update rails
``

or to update everything
```
gem update
```

## CamelCase or underscore ?

variable_name
method_name
ClassName
CONSTANTNAME

## Generate a new Rails project without test::unit, with postgres and git

```bash
rails new <your_project> --skip-test-unit --git --database=postgresql
```

## Ask Rails to create the database 
Remove user and password for all environments in database.yml file, or
```bash
createuser the_user
```

```bash
bundle exec rake db:create:all
```

## RSpec
In Gemfile : 
```ruby
group :development, :test do
  gem 'rspec-rails', '2.10.0'
end
```

then 
```bash
rails generate rspec:install
```

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
bundle exec rake db:rollback # single migration 
bundle exec rake db:migrate VERSION=0 # to the beginning
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

## Annotations to the code
You can annotate your code :

```
  # TODO: factor out model verification to a filter
  # OPTIMIZE: optimize this
  # FIXME: it's broken
```

and get all the annotations with :

```
bundle exec rake notes
```

