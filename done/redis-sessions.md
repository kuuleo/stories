# REF https://blog.dennisokeeffe.com/blog/2022-03-07-part-2-using-redis-sessions-instead-of-cookie-store

* [x] bundler add redis-rails
* [x] configure session store to use Redis by adding this to `config/initializers/session_store.rb`
```
Rails.application.config.session_store :redis_store,
                                       servers: ['redis://localhost:6379/0/session'],
                                       expire_after: 90.minutes,
                                       key: '_drifter_live_session'
```
* [x] start server
* [x] run `redis-cli monitor` to see get, del, & setex session from logging in and out
* [x] run `redis-cli flushdb` to remove all session_store
*on page refresh I should be redirected to login page
