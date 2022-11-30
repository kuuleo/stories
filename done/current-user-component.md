# The CurrentUser component is a Popover with the user slug or the user's name as the button text

* [x] put a placeholder in the button text for the user slug to go

* [x] use user circle icon and just make it plain black with text

* [x] current_user variable in the components template

current_user instance variable is accessable in all controllers with `before_action: authenticate_user!`.  Once I can access this user variable, ??HOW can I access it from a Rails view?

And, there should be some way to get data from a Rails view to a React component.  I think this is WHERE stimulus comes in.  Because right now, I putting the React component directly into the dom, so the component is not tied to a specifc Rails view.

With, Stimulus, I would use a tag.  I rememeber that one example I did used a conent tag.

* [x] check Stimulus docs on how to provide inputs from a Rails view to a stimulus controller...

REF https://blog.effectussoftware.com/stimulus-in-rails/
"... connects JavaScript objects = known as controllers = to elements on the page relying only on simple annotations"

REF https://stimulus.hotwired.dev/handbook/hello-stimulus
"... starts with HTML

At its core, Stimulus's purpose is to automatically connect DOM elements to JavaScript objects.  Those objects are called controllers.
"

* the root component can be the same file as the root stimulus controller
