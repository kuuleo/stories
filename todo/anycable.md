# Anycable instead of action cable for speed

REF https://gorails.com/episodes/test-rails-actioncable-with-devise?autoplay=1
*this is for regular devise with regular action cable... but first authenticate with devise... get that working and then apply to anycable*
Here is another REF for plain devise with plain actioncable authentication:
https://greg.molnar.io/blog/actioncable-devise-authentication/

* [ ] help  ⚠️  If you're using JS client make sure you have `action_cable_meta_tag` included before any \<script\> tag in your application.html

* [ ] Which environment do you use for development? (1) Local, (2) Docker, (0) Skip 1... I think...

* [ ] How do you want to install AnyCable-Go WebSocket server? (1) Homebrew, (2) Download binary, (0) Skip 1

Warden is middleware

Devise uses warden to authenticate

To make it work with AnyCable, you must add this middleware to AnyCable's middleware stack like this:

```
AnyCable::Rails::Rack.middleware.use Warden::Manager do |config|
  Devise.warden_config = config
end
```

REF docs.anycable.io/rails/authentication
Says that once I put the above in, I can access the current user.

Says I an initializier is one possible place to put the above code.

The way that I woudl acess the current user would be  `env["warden"].user(scope)` inside of the Connection class

And `scope` is "Warden scope" usually `:user`
REF github.com/wardencommunity/warden/wiki/Scopes

"A scope is identified by an object. (I would use a symbol usually)"

Rack is a layer between the framework (Rails) and the application server (Puma)

Rack is used so that frameworks and servers can be interchagable

Rack sits in the middle of every web request and response

A Rack application is a Ruby object (not a class) that responds to call.  It takes exactly one argument, the environment and returns a non-frozen Array of exactly 3 values: the status, the headers, and the body

The environment must be an unfrozen instance of Hash that includes CGI-like headers.  The Rack application is free to modify the environment.
* [ ] continue learning about Rack in this REF... but first get any cable installed per this other REF
* https://github.com/rack/rack/blob/main/SPEC.rdoc ... this is the REF on rack for trying to figure out HOW to authenticate the user in the anycable middleware
* https://docs.anycable.io/rails/getting_started... and here is the REF on getting anycable installed
* [ ] add `adapter: any_cable` for both production and development in "ActionCable configuration"... that's what he says in docs... I'll start there but maybe he means anycable configuration...??
*This line was already in cable.yml... I'm going to remove it and just have the above. I'm doing this because just in case it works, I want to know that it is anycable working and not what Rails is returning from the environment*
`adapter: <%= ENV.fetch("ACTION_CABLE_ADAPTER", "any_cable") %>`
*but i guess this means that erb works inside of yml files...??*

* [x] install WebSocket server and specify its URL in the configuration:
*vvvv I installed using brew install anycable-go vvvv*
```
# config/environments/development.rb
config.action_cable.url = "ws://localhost:8080/cable"
```

... and this for production:

```
# config/environments/production.rb
config.action_cable.url = "wss://ws.example.com/cable"
```

* [x] `bundle exec anycable` to start Anycable RPC server
```
Starting AnyCable RPC server (pid: 79352)
AnyCable version: 1.2.3 (proto_version: v1)
Serving Rails application from ./config/environment.rb
gRPC version: 1.50.0
Broadcasting Redis channel: __anycable__
RPC server is starting...
RPC server is listening on 127.0.0.1:50051 (workers_num: 30)
```
* [ ] start up `redis-server` from terminal

* [x] `anycable-go --host=localhost --port=8080` from terminal
vvvv
```
  INFO 2022-11-18T05:15:34.337Z context=main Starting AnyCable 1.2.1 (pid: 82161, open file limit: 256, gomaxprocs: 8)
  INFO 2022-11-18T05:15:34.337Z context=rpc RPC controller initialized: localhost:50051 (concurrency: 28, enable_tls: false, proto_versions: v1)
  INFO 2022-11-18T05:15:34.337Z context=main Handle WebSocket connections at http://localhost:8080/cable
  INFO 2022-11-18T05:15:34.337Z context=main Handle health connections at http://localhost:8080/health
  INFO 2022-11-18T05:15:34.339Z context=pubsub Subscribed to Redis channel: __anycable__
```

* [ ] `config/anycable.yml`
```
development:
  redis_url: redis://localhost:6379/1
production:
  redis_url: redis://my.redis.io:6379/1
```

* [ ] HOW do I want to do forgery protection... same as actioncable...??
REF anycable docs - "AnyCable rewspects ActionCable configuration regarding forgery protection if and only if `ORIGIN` header is proxied by WebSocket server"
```
# with anycable-go
$anycable-go --headers=cookie,origin --port=8080
```

??WHAT is the Action Cable configuration?
---> this should be the same as the part on allowed request origins...??


REF this on auth for regular Devise
https://greg.molnar.io/blog/actioncable-devise-authentication/

Rails docs say "The WebSocket server doesn't have access to the session, but it has access to the cookies. This can be used when you need to handle authentication."
And AnyCable will have the same access to cookies once I install that middleware config...?

it looks like it is working

* [ ] first try to make the same request to subscribe to IsOnlineChannel first thing... which should give me that same that can't find channel error

* [ ] next start with logging

* [ ] turn on access logs with
```
# config/anycable.yml
development:
  access_logs_disabled: false
```

* [ ] followed by forgery in the anycable docs
