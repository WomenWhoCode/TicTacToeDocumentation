# TicTacToe

Learn Rails through TicTacToe. It's test driven, fill in the blanks and...Have fun!

# Getting Started

* `Find the Repo here: https://github.com/WomenWhoCode/TicTacToeSkeleton`
* `Fork it, instructions here: https://help.github.com/articles/fork-a-repo`
* `Clone it to your computer`
* `Open the App in your text editor, i.e. Sublime or Komodo Edit`

# Gemfile

* `listed gem version defaults since each have different environments`

run...

~~~~
@@@ ruby

$ bundle install        
// installs any gems that you need, which are listed in your Gemfile

~~~~

# Migrations

~~~~
@@@ ruby

$ rake db:migrate       
// runs any migrations you have and sets up your database and datamodel

~~~~

take a look: /db/

Table: Game with a text column board

# Game.board

let's see our board 

~~~~
@@@ ruby

Array.new(3) { Array.new(3) }

~~~~

we'll view with the board next...

# Rails Console / Pry

* `gem 'Pry'`
* `syntax highlighting`
* `pry commands`

~~~~
@@@ ruby

$ rails c
>> wtf?
>> g = Game.new
>> g.board
>> g.display_board
>> ^d

~~~~

methods used here are found in app/helpers/games_helper.rb

# Board Validator

* `app/validators/game/board.rb`
* `makes sure board length is => Array.new(3) { Array.new(3) } and input 'o', 'x', nil`

# Players

meet 'o'

meet 'x'

# Running Tests...

~~~~
@@@ ruby
$ rspec spec/          
// runs all the tests in the project
~~~~

if you get errors, run 

~~~~
@@@ ruby
$ rake db:test:prepare
$ rspec spec/
~~~~

# Game model

* `app/models/game.rb`
* `spec/models/games_spec.rb`

# Resources

* `WWC google group`
* `Ruby Tuesday Core Team`
* `Railsbridge`
* `RubyMonk`
* `Codecademy`
* `Learn to Program`
* `Beginning Ruby`
* `RailsGuides`

!SLIDE

Come Again

# Updating routes.rb

in config/routes.rb

~~~~
@@@ ruby

resources :games
~~~~

~~~~
@@@ ruby

TicTacToe$ rake routes
    games GET    /games(.:format)          games#index
          POST   /games(.:format)          games#create
 new_game GET    /games/new(.:format)      games#new
edit_game GET    /games/:id/edit(.:format) games#edit
     game GET    /games/:id(.:format)      games#show
          PUT    /games/:id(.:format)      games#update
          DELETE /games/:id(.:format)      games#destroy
~~~~

# REST (Representational State Transfer)

User agents and servers transmit representations of resources between one another via a common interface (HTTP).  HTTP has seven methods, four of which are used by Rails in its RESTful routing.

Restful routes used by Rails:

* `GET: get a resource`
* `POST: create a new resource`
* `PUT: edit an existing resource`
* `DELETE: delete a resource`

For more information:
  https://en.wikipedia.org/wiki/Representational_state_transfer
  https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol


# GamesController

* The controller provides information from the model to the views, and passes messages from the views to the model.
* Controller methods utilize REST methods as well as calling methods on the model.
* Start by creating an index method which makes available all games that exist in the database:

~~~~
@@@ ruby

class GamesController < ApplicationController

  def index
    # provide all games in an instance variable
  end
end

~~~~

The other methods that we need are in the Games controller, waiting for you to fill them in!


# erb

erb is a library with which one can insert ruby code into HTML.  This code is all executed, but only the code on the line with the `<%=` is displayed on the page.

~~~~
@@@ HTML

// app/views/games/index.html.erb

 <% @games.each do |game| %>
 <%= game.inspect %>
 <% end %>
~~~~

# params

To simplify things a bit, params are part of the information passed between server and user agent.  In Rails they are treated as a hash. For example, when viewing the games index page and wanting to view a game, if you click on that game, in the following code the id of the game is stored in the params hash, and accessed by the controller's show method, which makes it available to the view by putting it in an instance variable:

~~~~
@@@ HTML

// in app/views/games/index.html.erb

  <% @games.each do |game| %>
    <%= link_to show_path, id: game.id %>
  <% end %>

~~~~

~~~~
@@@ ruby

// app/controllers/game.rb

  def show
    @game = Game.find(params[:id])
  end

~~~~
See also: http://stackoverflow.com/questions/6885990/rails-params-explained
http://rails.nuvvo.com/lesson/6371-action-controller-parameters

# partials

There are many partials in our views.  Take a look at app/views/layouts: any file that starts with an underscore is a partial.  The application layout itself could be considered a partial.  Partials contain snippets of view code which can be inserted into any other view file.  Partials are code that will be used over and over again in the views, or are for any other reason more easily dealt with when separated from the main view; an obvious example is the application layout, which is used on every page. 

We've extracted things such as the header, footer and shim (code to provide help for Internet Explorer browsers that don't have support for HTML5) from the application layout in order to make them easier to edit.  In some applications, though not ours at this moment, the application layout is a huge file, and separating out these crucial elements makes them easier to find and edit when the need arises.

We've also created a partial to be used in our TicTacToe board - app/views/game/_board_form.html.erb.  Can you see where it might be used?

See also: http://guides.rubyonrails.org/layouts_and_rendering.html#using-partials
