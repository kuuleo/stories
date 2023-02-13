Devise/Warden
Devise relies on warden Rack middleware to authenticate users.

In order to make it work with AnyCable, you must add this middleware to AnyCable's middleware stack like this:

AnyCable::Rails::Rack.middleware.use Warden::Manager do |config|
  Devise.warden_config = config
end
Copy to clipboardErrorCopied
You can put this code, for example, into an initializer (config/initializers/anycable.rb) or any other configuration file.

Then, you can access the current user via env["warden"].user(scope) in your connection class (where scope is Warden scope, usually, :user).

REF https://docs.anycable.io/rails/authentication
