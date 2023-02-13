# LiveView for a context per the REF Programming Phoenix LiveView

Here was the modification to the on_mount callback in user_auth_live.ex

```
socket = assign_new(socket, :current_user, fn ->
      Accounts.get_user_by_session_token(user_token)
    end)
```

It was originally like this after the auth part from chapter 2
```
socket =
      socket
      |> assign(:current_user, Accounts.get_user_by_session_token(user_token))
```

* [x] save an empty template in lib/drifter_web/live/shops_live.html.heex

* [x] add thes debugging statements to DrifterWeb.UserAuthLive.on_mount/4 callback

MIND by adding that alias __MODULE__.Component line to the first line of the ShopsLive module, I guess that means that I will have a tag available for Component in that LiveView


... so if I want to have that Components file working, I would want to have an alias for that __MODULE__.Components in the main module instead of a context module...??

But before, I had a method for greet and in this tutorial, they have a method for mount...
??WHERE does the mount method get called?

... I found the REF using the greet method with the attr.  It is dated November 2022 so it's pretty new.  It should be using the later versions of Elixir and Phoenix.

In this tutorial, the greet method also becomes the name of the component like this:

`<.greet />`

It says that the `attr` is from the `Phoenix.Component` module so maybe if I have that Component imported, then attr will work...??
---> The `attr/3` is available in the 0.18 versions and I'm running 0.17.12.  I don't see the **Attributes** section in the docs for 0.17.12

If I put .greet into one of my templates right now, will the component show?

??WHAT is the module that the Components file is in?
... well it is in the drifter_web directory and there isn't an index-like or main-module file that I found... unless it is in the parent directory
... in the parent directory, there is a drifter_web.ex file...
... and in this file, this is in there:
```
  def component do
    quote do
      use Phoenix.Component

      unquote(view_helpers())
    end
  end
```

* [ ] try just putting the greet component in there and follow the dos for 0.17.12
I aliased in that example because my `defmodule` was DrifterWeb.ShopsLive.Component... actually I changed it to DrifterWeb.ShopsLive.ShopThing just to see HOW it works...
... heex files and I can put my components in them...??
... well I guess let's find out...
* [ ] try putting <Components.greet inside of user_menu.heex
... I should get an error for not having values for the assigns...
... yeah... I got this:
```
** (KeyError) key :name not found in: %{__changed__: nil}
        (drifter 0.1.0) lib/drifter_web/components.ex:9: anonymous fn/2 in Components.greet/1
```
