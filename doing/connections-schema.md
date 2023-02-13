 # I have a Context called Circles that contains a Schema called Connection that models my user connections

 * [ ] create a connections migration and Connection schema using the generator
 mix phx.gen.context Circles Connection connections accepted:boolean \
 sender_id:references:users receiver_id:references:users
 
 vvvv WHEN I ran the above command, it is asking me to overwrite.  I'm going to overwrite and and see WHAT the new code is...

 Here is the old code from connection.ex

 defmodule Drifter.Circles.Connection do
  alias Drifter.Accounts.User
  use Ecto.Schema
  import Ecto.Changeset

  schema "connections" do
    field :accepted, :boolean, default: false
    belongs_to :sender, User
    belongs_to :receiver, User

    timestamps()
  end

  @doc false
  def changeset(connection, attrs) do
    connection
    |> cast(attrs, [:sender_id, :receiver_id, :accepted])
    |> validate_required([:sender_id, :receiver_id, :accepted])
  end

* [x] use this belongs to format and add unique constraint on the index of sender/receiver ids

... also, it might also alter the circles.ex file so here is that existing code:

defmodule Drifter.Circles.Connection do
  alias Drifter.Accounts.User
  use Ecto.Schema
  import Ecto.Changeset

  schema "connections" do
    field :accepted, :boolean, default: false
    belongs_to :sender, User
    belongs_to :receiver, User

    timestamps()
  end

  @doc false
  def changeset(connection, attrs) do
    connection
    |> cast(attrs, [:sender_id, :receiver_id, :accepted])
    |> validate_required([:sender_id, :receiver_id, :accepted])
  end
end

... also, WHEN I overwrite, it might recreate the migration so here is the current migration file... which is the one I'm interested in seeing HOW to write to include the self referential association correctly 

* [x] cast all 3 columns in the connection.ex
* [ ] validate_required for all 3 columns
