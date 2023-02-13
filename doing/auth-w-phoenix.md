# Authentication with the baked in Phoenix auth

REF https://github.com/aaronrenner/phx_gen_auth/

REF https://github.com/dashbitco/mix_phx_gen_auth_demo/pull/1
REF https://dashbit.co/blog/a-new-authentication-solution-for-phoenix


GROOVE In order to prevent user enumeration attacks, don't disclose whether the email is registered

* [ ] add a key to the socket.assigns for the lib/drifter_web/live/

@impl means the function implements a callback...??

I added the part for directly accessing session and current user in the assign function.  Since I don't have a wrong.ex, I tried to put it into the index.ex file.  But I think there should be some other stuff to make it really work.  Since that part is just for demo purposes, skip it and got to:

* [ ] define a module that implements an `on_mount/4` at `auth/drifter/lib/drifter_web/live/user_auth_live.ex`

* [ ] get the session_id from the index.ex...

??HOW to define assigns functions?... WHICH assign coordinates with that specific assigns?... HOW do it modify that assigns function that is tied to the index.html.heex assign that is in the mount function?


* [x] posts/XXX live views inside of live_session
```
live_session :default, on_mount: DrifterWeb.UserAuthLive do
  live "/posts", PostLive.Index, :index
  live "/posts/new", PostLive.Index, :new
  live "/posts/:id/edit", PostLive.Index, :edit

  live "/posts/:id", PostLive.Show, :show
  live "/posts/:id/show/edit", PostLive.Show, :edit
end
```

* [x] DrifterWeb.UserAuthLive... module that implements an `on_mount/4` function
```
defmodule DrifterWeb.UserAuthLive do
  import Phoenix.LiveView
  alias Drifter.Accounts

  def on_mount(_, params, %{"user_token" => user_token} = _session, socket) do
    socket =
      socket
      |> assign(:current_user, Accounts.get_user_by_session_token(user_token))
    if socket.assigns.current_user do
      {:cont, socket}
    else
      {:halt, redirect(socket, to: "/users/log_in")}
    end
  end
end
```

* [ ] put a svg directly into a ~H"""""" for the drifter logo

* [ ] add the other stuff at the end of the auth chapter to the backlog
