# shareLocation epic triggered by user.sharingLocation == true

* [ ] sharing location toggle set to true dispatches an action shareLocationRequest

* [ ] shareLocationEpic

* [ ] sends slug and sharing location: true to redis

* [ ] sharing location starts sending navigator to redis which will modify my current user hash in redis which will have timeout attached to it

* [ ] stops ending location update when the user offline action is received

* [ ] stops sending location updates when the toggle is switched back to location hidden

* [ ] if user isOnline:false because of timeout sharing location is still set to true but location coordinates stop being sent to redis

* [ ] sharingLocation should start as false but shouldn't be set to false everytime the user is inactive.  can be sharingLocation:true isOnline:false and these settings cause coordinates to stop being sent

* [ ] changes to the user hash including the lcoation coordinates will reset the timeout location for user is isOnline

* [ ] client side keeps a time and stops sending coordinates

* [ ] redis also keepas a time because of the hash timeout and deletes user hash from memory

* [ ] setIsActive starts the timer in the fronend

* [ ] setIsActive sends message to backend that user is online

It will be the dom events that trigger the setActive action and once that observable starts, I want the next event that would go into the pipe to cancel the last one.  So that would mean I can use switchMap and the map it to the outgoing action

* [ ] have the dom event trigger the action...

WHEN would I want to track activity while the user is not sharing his location?  WHEN I want to let the server know that I'm online

So I'm going round trip
