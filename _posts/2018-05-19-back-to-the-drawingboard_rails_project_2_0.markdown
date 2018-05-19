---
layout: post
title:      "Back-to-the-Drawingboard Rails Project 2.0"
date:       2018-05-19 18:37:20 +0000
permalink:  back-to-the-drawingboard_rails_project_2_0
---


I had my rails project review about two months ago and suffice to say that it didn't go as I hoped. I'll be honest and say that I went into my rails project not having the best grasp on certain concepts(which i'll touch on later) but I figured that I would forge on ahead anyway. When I was asked at the end of my review and I was to refactor a few things I thought it would be easy but my lack of knowledge made that complicated.

That was when I also realized that making the neccessary changes wasn't only difficult because of my lack of understanding but because of the lack of simple logic that I used when building my project. What exactly do I mean by lack of simple logic ? Well if it's not easy for you to explain the idea of your project and how to works that's usually a red flag also if your model association lack simple logic that's a red flag also. So let's get into where I went wrong and how I fixed how those issues.

My original logic for my project was to have a web application that would let users also known as film fans saved their favorite directors through those directors they could save movies through directors made. They could also view those movies by movies they've watched and movies that they consider to be their favorite films.

The *directors* directly belonged to the *user* and the *movies* then belonged to the director. This made sense to me until I got to the point in my project where I had to set up a join table and the only thing I could think of was having a has_many relationship between the movies and genres. So my has_many through relationship looked like this:

```
class Movie < ApplicationRecord
  has_many :genres, :through => :movie_genre
end
	
class Genre < ApplicationRecord
  has_many :movies, through: :movie_genre 
end	

class Director < ApplicationRecord
 has_many :genres, through: :movies
end
```

So what doesn't make sense here? well a movie doesn't have many genres it has one genre and a directors doesn't have many genres either. That should have been a red flag but I pushed through because I couldn't think of anything else at the time. However, with time and effort came wisdom lol. So I thought of other attributes that movies have that could be better suited for a has many thorugh relationship association. That's when I came up with the *comments* attibute. 

A movie can have comments and a user can have many commented movies. Now this idea has logic!

```
class User < ApplicationRecord
 has_many :commented_movies, through: :comments, source: :movie
end

class Movie < ApplicationRecord
 has   has_many :comments, dependent: :destroy
end
```

With this change I also had to add a Comment model (with a belongs to relationship with the user nad model model) and comments migration. I, then, had to set up a has many relationship between the User and Movie model and the User and Comment model. With this changes I started to think about why I had a belongs to relationship between my Director and Model movie. 

The original issue I was having with my project was being able to refactor a scope method. I had a scope method set up as a separate controller instead of in my model. Like so:

```
class Movies::WatchedController < ApplicationController
 def index
@movies = Movie.where(director_id: current_user.director_ids, user_watched: "Yes")
  end
end
```

What I needed was something like:

`scope :user_watched -> where(user_watched: "Yes")`

The difficultly in refactoring came when I tried to access my association relation of user_watched movies. Because my Movie model was only associated to my User through the Director. I had some hoops to jump through as shown when tried through my rails console.

![](https://imgur.com/a/xRbGNWz)

With adding the changes I did to my user and movie model I was able to add a newest_movies scope.
`scope :newest_movies, -> { order('created_at desc').limit(5) }`

Not passing a review is a blow but when you take a step back you can learn a lot. I went back to review Model Class Methods, Nested Routes and Restful Routes as well. I'll probably write a blog post on those as well. 

Check out the changes I made to my project[ here](https://github.com/Eclecticdynasty/film-fan-rails).






 




