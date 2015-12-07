# Rails API + React
* Step by step guide in creating a Rails API only application with React JS as front-end

## Prerequisite
1. Download `Postman` Google Chrome Application to test API Endpoints

## Rails API

### Set Up
1. Install `rails-api` gem
  * `gem install rails-api`
  
1. Generate a new Rails API application
  * `rails-api new [app_name]`
  * check `rails-api new --help` for other options
  * Note of the structure of your new rails-api application, the `view` directory is missing since this is an API only application

1. Generate `models` as you usually do on a normal rails application
  * `rails g model [model_name]`

1. Generate `controllers` as you usually do on a normal rails application
  * `rails g controller [controller_name]`
  * Note that this generator will not create any view files
  * Note also that `ApplicationController` inherits from `ActionController::API` instead of `ActionController::Base`

1. Define `routes` as a usual rails application
  * most probably you won't be needing `new` and `edit` routes
  
1. Return for each controller action should be `json` object
  ```ruby
    def index
      render :json => User.all
    end
  ```

1. Start your rails server and test your API Endpoints using `Postman`
  * Take note of the responses, it is not pretty and not formatted
  * To adjust the formatting of the responses, we can use `Active Model Serializers`

1. Install `active_model_serializers`
  * Add `gem 'active_model_serializers', '~> 0.9.3'` to your `Gemfile` and run bundle install

1. Generate Serializers for your resource
  * `rails g serializer [resource]`
  
1. Define the serializer for your resource
  ```ruby
    class UserSerializer < ActiveModel::Serializer
    
      attributes :name, :email
    
    end
  ```
  
1. Include Serialization module in `ApplicationController`:
  ```ruby
    class ApplicationController < ActionController::API
      include ActionController::Serialization
    end
  ```
  
1. Restart your server and test your API Endpoint again, you should see the defined attributes only

## React
