# React app running using Phoenix

## Phoenix
REF https://dev.to/lionelmarco/elixir-plug-cowboy-websockets-broadcasting-to-react-46if
REF https://dev.to/siddhantsingh/cache-the-data-using-redis-in-elixir-phoenix-280d
REF https://docs.statetrace.com/blog/redis-server/
REF https://www.udemy.com/course/the-complete-elixir-and-phoenix-bootcamp-and-tutorial/learn/lecture/5941630#overview

# Elixir and websockets
REF https://thoughtbot.com/blog/playing-with-sockets-and-processes-in-elixir
REF https://furlough.merecomplexities.com/elixir/phoenix/tutorial/2021/02/19/binary-websockets-with-elixir-phoenix.html
REF https://dev.to/darnahsan/real-time-dashboard-with-websocket-in-elixir-5ald
REF https://medium.com/@loganbbres/elixir-websocket-chat-example-c72986ab5778

## Authentication websockets in Elixir
REF https://medium.com/caspertechteam/securing-websockets-in-elixir-770cbd2da043

## Phoenix with React
REF https://dev.to/ndrean/use-phoenix-to-run-react-20e3
REF https://github.com/srozen/phoenix_react_typescript/blob/master/assets/js/components/dummy.tsx
REF https://blog.nootch.net/post/react-and-phoenix-liveview-2022/

## Go with redis (at the end of the day I want Elixir with Redis)
REF https://itnext.io/lets-learn-how-to-to-build-a-chat-application-with-redis-websocket-and-go-7995b5c7b5e5

* [x] change the database user from postgres to drifter

vvvv I ran the server using mix phx.server and at first it errored because I hadnt' run the migration.  The weird thing was that it was difficult to to quit the application.  I would hit ctrl c and there would be some options.  I tried to kill but that didn't work.  Then I did Abort with capital A and that seemed to work.  But the weird part was that the errors was saying something about no route for my/chat.  This was the route from the first demo app that I had made that is in another directory.  So I guess I hadn't quit that one properly.

* [ ] got back to the tutorial for the first app and figure out how to close that app out 

* [ ] figure out what process is still runnning and how to stop it...

?? in REF blog.nootch.net/post/react-and-phoenix-liveview-2022/
he renders a component inside of a def render function just like the twiiter clone...??

No, Chris McCord created a component in the resource directory under the live directory.  The component is an ex file.  It has a render function that has erb looking html inside it. 

"instead of saying once event X happens, change Y on the page... events in LiveView are regular messages which may cause changes to its state.  Once the state changes, LiveView will re-render the relevant parts of its HTML template and push it to the browser... The flipside is that LiveView uses more memory on the server compared to stateless requests"

If 50 million users could all have a state at any given moment... or the server could have sent it out and forgot about it

Not to say there shouldn't be some, but I don't want on for each time there is async data.  It makes more sense to have one for every group of information that I want to keep track of. The main point being that I don't want to drill down to find things in the cache(Redis) of the entire app

Online users in the form of and entity so that a user can get his online_contacts

... using (noothces) tutorial, I got not errors and no React... WHERE is my feedback...??

??WHERE is that other file... the one that says Here be some React?

* [ ] try this ref to see React
REF https://betterprogramming.pub/phoenix-1-6-with-typescript-react-bea7f3a792d5

* [x] create app using umbrella "says it harder to got from reg app to umbrella later than other way around"
`mix phx.new drifter --live --umbrella --database postgres --binary-id`
