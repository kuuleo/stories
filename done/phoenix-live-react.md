# I have React components that process data using LiveView inputs and outputs

REF github.com/fidr/phoenix_live_react

* [x] make a LiveView that is at the url "/"


So to get a live view, Live routes defined with a call to the live/3 macro, map incoming http web request to a specified live view so that a request to that endpoint will start up a live view process

That process will initialize the live view's state by setting up the socket in a function called mount

Then the live view will render that state in some markup for the client.

This initial http request and response flows through the live route.

After that, a persitent websocket connection will handle the liveview communication.

I guess that the format is ("Components.Map", [props go in here... so stuff that change based on the stuff coming in only on the websocket], id: "... and I guess here's the id")

actually websocket should be full duplex so a number should be able to go in and user should be able to change the number an then the number should come out of the component through the websocket

vvvv map is showing
... the size is full size, but it is offset instead of covering the screen

but home is not a live view... it is a WHAT?



so @inner_block is a slot
... so I guess that means I can say:
<.some_function_component inner_block={someHtmlVariable}...??

... no... I just write the component as <.component> PUT HTML HERE </.component> ... and the stuff in between(html) gets shown inside the component
... and I guess those slots could all be markers... and the stuff inside the popup I want can be sent to the slot


live_session(name, opts \\ [], list)... defines a live session for live reirects within a group of live routesj


    That should get rid of the spacing I've been trying to get rid of

    I'm just trying to get rid of spacing

There is a format for LiveView that uses :app

"All of the imports and aliases we make in our module will also be availabel in outr templates... because templates...compiled into functions inside their module..."  So that means that:
 - if I use HelloWeb.HelloHTML
 - and I embed_templates "Hello_html/\*"
 - then I can call those templates using :template_name inside of the module HelloWeb.HelloHTML
 - and in the router, I'm using the module DrifterLiveWeb.Layouts... which is a module
 - so since those templates are in that module, I can call :app or anyother file name in that embed_templates directory
 - so if I want to use map as one of the layouts, I should put that as one of the templates in layouts
 - or I could just put in the function component into one of the layout files

I put this class in the index file:
fixed inset-0 h-screen flex justify-center items-center

... and it is contained in the app template which has a relative class
```
<main class="relative">
  <p class="alert alert-info" role="alert"><%= get_flash(@conn, :info) %></p>
  <p class="alert alert-danger" role="alert"><%= get_flash(@conn, :error) %></p>
  <%= @inner_content %>
</main>
```


... and then this is housed inside the root.html.heex... insidre the body tag, but the body tag does not have any styling

this was in the map liveview... i just took it out

    <div class="fixed inset-0 h-screen flex justify-center items-center">

??now what is the map liveview's containing element?

... it is still phx-update="ignore"

* [x] try moving the classes that are currently on map directly to the liveview html

?? now WHICH element has those classes?
---> the one wrapping the react element
* [x] git the one wrapping that one the class that does the h-screen thing
