---
layout: post
title:      "Rails Project"
date:       2018-03-10 19:26:35 +0000
permalink:  rails_project
---


For my rails project I wanted to build upon what I built for my sinatra project but with a few changes. I wanted my app to be less like a forum and work more like a database for film fans to keep track of their favorite directors and the films from those directors. With my Sinatra project I tried to outline starting from the migrations then models, controllers and lastly, views.  However I had to take a different appraoch with this project. With the requirements of having a has_many: :through relationship in one of my models, at least one level ActiveRecord Scope method (which I'm still not sure if i understand at this point) and a nested form that writes to an associated model through a custom attribute writer. I decided to start outlining my models.

I was able to come up with a join table *movie_genre* as my has_many: :through relationship. 

```
class Movie < ApplicationRecord
  has_many :genres, :through => :movie_genre
end
	
class Genre < ApplicationRecord
  has_many :movies, through: :movie_genre 
end	
```



For my Active Record scope methods, I added a user_watched feature and a favorites feature.
	
	
	
```
class Movies::WatchedController < ApplicationController
 def index
@movies = Movie.where(director_id: current_user.director_ids, user_watched: "Yes")
  end
end

class Directors::FavoritesController < ApplicationController
  def index
    @directors = current_user.directors.where(rating: 5).order(:name)
  end
end
```
	
Once I had those two things mapped out, it was pretty smooth sailing from there. My project took me about 14 days. I had a bit of a hiccup with genres migration. I was trying to make a Format/genre relationship like there is for Media/Medium but I had to realize that rails doesn't recognize format to be the plural for genre. 

Overall, building this project has been fun and I got to play around with the css again; with this project I wanted to use tables and keep the css as simple as possible. 

Repo for my Rails Project [here](https://github.com/Eclecticdynasty/film-fan-rails)
	


