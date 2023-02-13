# Twitter clone using pure Phoenix


* [x] add live routes for posts... make sure the route format is the same as this REF:
https://github.com/Morzaram/phoenix-twitter-example-1.6/blob/main/lib/chirp_web/router.ex

* [x] form.component.html.leex... is the video... check format of (Morzaram) REF
vvvv same I have mine saved as heex and text is the same as (Morzaram's)

* [x] modify the timeline for post for schema and ...

* [x] post_live/index.html.heex that gets the posts as they come in WhHEN a contact tweets

* [x] DrifterWeb.PostLive.PostComponent... to get the post template showing

* [x] modify drifter/timeline.ex for the broadcasts in the create_post and update_post streams

* [x] add a temporary_assigns to the PostLive.Index mount method so that I can update the individual posts without have to find it first
"We throw it away and make it and empty array before we render... temporary assigns"
??WHAT is the IO.XXX stuff for that the updated github REF has for the handle_info update method?

* [x] add the prepend to the index.html.heex... so it is only prepending new children and not replacing all the old children(posts)

??WHY is my update sending an update every time I type in the form...?

I think the form for the component is DrifterWeb.PostLive.PostComponent

* [x] compare my timeline files with the github example I have and look for differences that would trigger an update action every time I type... (Chris's) only update WHEN he hits save
vvvv I ran the example, and his is doing the same thing with the update showing up...

I'm still not sure WHAT that IO in the code does...
... When I update a post, WHY is it updating every keystroke and then WHEN I hit save, it does a mount... should be the timeline file...

... maybe it's because I don't understand the assigns...

* [x] add delete to my drifter/timeline.ex
