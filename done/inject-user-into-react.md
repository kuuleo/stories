# As a user, I see my current user data and settings WHEN I hover over the navbar button with my slug/name
* [ ] add friendly id with slug returning the user slug so that I can use it to display slug in the user button in the case that a name is not present
REF https://github.com/norman/friendly_id
* [x] bundle add friendly_id
---> added 5.4 to the Gemfile

* [x] rails g migration AddSlugToUsers slug:uniq

* [x] rails g friendly_id
---> I left `CreateFriendlyIdSlugs` in the migrations/ slugs table was created

* [x] add the friendly_id method for slugs that I have in drifter_api
```
  extend FriendlyId
  # :finders make User.find('eneida') and User.active.find('eneida') work
  friendly_id :slug_candidates, :use => [:slugged, :finders]

  def slug_candidates
    [
      :initial_slug,
      [:initial_slug, :random_number],
      [:initial_slug, :bigger_random_number]
    ]
  end

  def initial_slug
    self.email.split("@")[0]
  end

  def random_number
    rand(9)
  end

  def bigger_random_number
    rand(99)
  end
```


* [x] from rails console do `User.find_each(&:save)` to add slugs to all user rows that have already been created before installing friendly_id

* [x] App component puts the user data into the store

* [x] CurrentUser component retrievs the user from the store

* [x] display the slug next to the tb user circle in the right corner

??HOW to write reducers WHEN I'm using the createSlice function?
I'm specifically wondering about the part using reducers.  If my action has a payload user, HOW can I get the user to become the user state.  Especially since the attributes isActive and isOnline do not come from the backend.  They are already part of the intial state with default `false` values.

* [x] add an interface for User with name as optional

* [x] add the logic that displays the slug when a name is not present

* [x] display the user's name next the user circle icon


* [x] make a stimulus home that gets a static value current-user

