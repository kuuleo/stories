# userOnline action triggers connection to websocket request using connectWebSocket epic

* [ ] is online based on the component I made in Angular with a timeout

* [ ] toggle so users can decide whether their people can see if they are online

* [ ] toggle turned on text "Visible, my contacts can see that I'm online"
* [ ] toggle turned off text "Invisible, my contacts cannot see that I'm online"


I'll go round trip for this one too... and for Activity/Inactiviy

For online, I call an action called: `connectCableRequest` from the IsOnlineComponent
* [ ] check what that request triggers... it does this:
```
  connectCableEffect$ = createEffect(() =>
    this.actions$.pipe(
      ofType(CableStoreActions.connectCableRequest),
      switchMap(action => of(action).pipe(
        withLatestFrom(this.store$.pipe(select(AuthStoreSelectors.selectAuthData)))
      )),
      map(actionArr => actionArr[1].access_token),
      switchMap(accessToken => this.cableService.connectWebSocket(accessToken)),
      map(event => this.cableService.setActionType(event)),
      switchMap(event => [
        event
      ]),
      catchError(e => {
        this.toastr.error(e.errorStatusMessage);
        console.log(e);
        return of(CableStoreActions.connectCableError());
      })
    )
  );
```

* [ ] ??WHAT does cableService.connectWebSocket(accessToken)) do?... I'm thinking one option is to do the same thing just without a access_token
*I should be able to just make a request to the path... or do I have to use the entire url since it is WS or WSS?*

* [x] add redis to gemfile

* [ ] get the url I was using in drifter.live/drifter environment file... the angular one

* [x] add this to routes
` mount ActionCable.server, at: '/cable'`

Even with just the standard documentation for Rails, they are still making a request to establish a connection.

Now, I just want to see the cable message in the console like I normally do... and I think it should still show up even though I'm running bin/dev...??

According to Rails docs, the connection won't connect until a subscription has been made...??

... and a subscription is just a perform...

... and I have to first connectCableError

In data or network communciation, a frame is a data transmission unit with a header indicating the beginning and end of a block of data

* [ ] development url for cable connection is ??WHAT?
`cableUrl: 'ws://localhost:3000/cable'`

* [ ] restart server after adding the cable to routes

The Connection file is currently empty:
```
  class Connection < ActionCable::Connection::Base
  end
```

So that should mean that it will connect without any authentication.

* [ ] make the connection using websocat in the terminal to `ws://localhost:3000/cable`

I have a window event that triggers isOnline and online action should trigger the connect websocket action

* [ ] in websocket key should also be a feature

* [ ] connection epic that listens for userIsOnline action and responds with the websocket subject request

* [ ] the websocket subject opens the pipe which just emit actions

* [ ] userOnline action triggers cable connection in connection epic

* [x] define checkOnline action in user/slice

* [x] put the <IsOnline /> component in the App component

