# REF https://blog.dennisokeeffe.com/blog/2022-03-07-part-1-setting-up-devise-with-rails-7

* [x] new Rails 7 app bundled/drifter
8 [x] bundler add part-1-setting-up-devise-with-rails-7
* [x] bin/rails g devise:install
* [x] bin/rails g devise User
* [x] bin/rails generate controller components/index
* [x] add this to `config/environments/development.rb`
`config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }`
* [x] add this to `app/controllers/application_controller.rb`
```
class ApplicationController < ActionController::Base
  before_action :authenticate_user!
end
```
* [x] set this as routing
```
Rails.application.routes.draw do
  devise_for :users
  # Define your application routes per the DSL in https://guides.rubyonrails.org/routing.html

  # Defines the root path route ("/")
  root 'components#index'
end
```
* [x] uncomment out line in devise initializer starting with `config.navigational_formats`
* [x] add `:turbo_stream` to the array in this line

* [x] modify `app/views/components/index.html.erb` by adding this line to the end
`<%= link_to "Log out", destroy_user_session_path, data: { "turbo-method":
4:delete } %>`

* [x] setup and migrate the database
`bin/rails db:create db:migrate`

* [x] start server `bin/rails s`
