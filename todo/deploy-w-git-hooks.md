# This is how I did it before... and its seems good and straight forward... so let's plan on it unless something better comes along

* [ ] start up redis server as on of the tasks
??WHICH --- same as in dev `redis-server` --- or some other way since it is production...??
* [ ] add this to one of the deploy tasks
`RAILS_ENV=production bundle exec anycable`
