# make an epic that listens for init action or checkIsOnline action which triggers the cable to try to connect with the webSocket service

* [ ] make a webSocketConnected action in main reducer

* [ ] I think I have to map () => connected() to execute the connected function/action and I don't think I'm doing it now... I can also try the mapTo using the string for the type 'webSocket/connected'...

* [ ] put the selector value for isOnline changing to run the effect in websocket component

* [x] make a cable request directly from WebSocket component by directly subscribing to the stream inside of the components useEffect() function
```
useEffect(() => {
    const webSocketStream$ = webSocket({
      url: 'ws://localhost:3000/cable'
    })

    webSocketStream$.pipe(
      tap((data) => console.log(data)),
    ).subscribe()

    return () => {
    }
  }, [])
```

* [x] find a subscription made in the Angular app where the action was for isOnline
`this.store$.dispatch(SubscriptionsActions.subscribeToChannelRequest({ channelIdParams: { channel: "IsOnlineChannel" }}));`

* [x] ??WHAT does this action trigger?
---> it triggers this effect
```
subscribeToChannel$ = createEffect(() =>
    this.actions$.pipe(
      ofType(SubscriptionsActions.subscribeToChannelRequest),
      tap(action => {
        const subscribeCommand = {
          command: 'subscribe',
          streamIdNameParams: action.channelIdParams
        };
        this.cableService.sendCommand(subscribeCommand)
      })
    ),
    { dispatch: false }
  );
```

* [ ] ??WHAT does sendCommand do?
---> it does this from cable.service
```
sendCommand(toDo: CableCommand) {
    const command = toDo.command
    const identifier = JSON.stringify(toDo.streamIdNameParams);
    const data = toDo.data ? JSON.stringify(toDo.data) : undefined;
    return this.wsSubject.next({command, identifier, data});
  }
```

So that means channelIdParams is this: { channel: "isOnlineChannel"}

I created an interface called CableCommand
```
export interface CableCommand {
  command: string;
  streamIdNameParams: ChannelIdParams;
  data?: any
}
```

Which now looking back is all just plain confusing...

I'm doing webSocketStream$.next({
  command: 'subscribe',
  identifier: JSON.stringify({
    channel: "IsOnlineChannel"
  }),
  data: OPTIONAL IF THERE IS ANY
})

... and before I forget
* [ ] put the stream in the middle in an epic so that an action can deliver these subscriptions requests to certain channelIdParams
* [ ] ... and the output of the epic can deliver the stuff coming back from the websocket

As @skyboyer has written in a comment under your question, you could use useRef hook to hold WebSocket and it will be more correct since you are not going to change or recreate WebSocket object. So you don't need useState hook.

The useRef() Hook isn’t just for DOM refs. The “ref” object is a generic container whose current property is mutable and can hold any value, similar to an instance property on a class. more

So you could change your code to:

const Chat = () => {
    const [messages, setMessages] = useState([]);
    const webSocket = useRef(null);

    useEffect(() => {
        webSocket.current = new WebSocket("ws://url");
        webSocket.current.onmessage = (message) => {
            setMessages(prev => [...prev, message.data]);
        };
        return () => webSocket.current.close();
    }, []);
    return <p>{messages.join(" ")}</p>;



* [ ] useRef hook to make a REF to the webSocketSubject instance

* [ ] useRef inside of epic

For epics, I don't want to request a connection if there is not need to.  And the connection doesn't do anything until there is a subscription.

Everything is triggered by a request.  There is a request to connect followed by a request to subscribe to a channel.  There are requests to send data to a channel.

Then there are things that happen with a websocket without doing anything.  Data just comes in. 

* [ ] define the types per the redux toolkit docs so that cableResponse has a payload with the data returned from action cable even though this action does not modify the webSocket useState

* [ ] utility function that sorts the cable data and puts it in the proper place in the store

* [ ] dispatch a cableRequest with 
```
{
    command: 'subscribe',
    identifier: JSON.stringify({ channel: 'IsOnlineChannel' })
  }
```

* [x] make an interface for cableRequest

* [ ] make an interface for CableResponse... with fields necessary to sort the data coming back into the store

* [ ] add the actionpayload thing to cableResponse too

* [x] dispatch cableRequest action from the IsOnline component
```
{
  type: "webSocket/cableRequest"
  payload: {
    command: "subscribe",
    identifier: JSON.stringify({
      channel: "IsOnlineChannel"
    })
  }
}
```

This function is in my angular service:
```
  sendCommand(toDo: CableCommand) {
    const command = toDo.command
    const identifier = JSON.stringify(toDo.streamIdNameParams);
    const data = toDo.data ? JSON.stringify(toDo.data) : undefined;
    return this.wsSubject.next({command, identifier, data});
  }

```

* [ ] do this same thing inline in the epic

* [ ] check for an instance using withLatestFrom and return it  instead of creating a new instance of websocket if there already is onmessage
* [ ] use withLatestFrom to retrieve the instance from the store
*I could possibly avoid withLatest from if I just start streaming from WHATever this epic returns*

* [ ] ~~first just confirm that the instance is getting saved to the store~~
*didn't get saved... maybe I'm doing it wrong but fucking with it could suck my life away*

This is working...
* [ ] delete all the unrelated todos and move to done
