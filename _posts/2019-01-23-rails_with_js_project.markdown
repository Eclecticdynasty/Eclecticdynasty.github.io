---
layout: post
title:      "Rails with JS Project"
date:       2019-01-23 21:34:51 +0000
permalink:  rails_with_js_project
---


The process of learning JavaScript was quite challenging for me. Which isn't surprising since there hasn't been a programming/scripting language that has been a cakewalk to learn thus far. The true test of whether or not I have a pretty good understanding of what I've learned are usually a project so it was time to put my knowledge to the test.

I decided to work on this project going requirement to requirement. Since it was a project about building upon what I had already built instead of building a new app from the ground up. One requirement that was most challenging was the 4th requirement.
	
*Must use your Rails app and JS to render a form for creating a resource that submits dynamically*
	
The part of it that was challenging was building out the object and prototype for creating a new comment. This made me go back to review JS concepts. Particularly, Objects, Object Methods, and Prototypes. 

A prototype is a JS object. That object can have specific attributes. After getting a better understanding I went on to this about what my Comment object should do and therefore what specific attribute my comment would need. I wanted to be able to append a comment body with the commenter's username to the class element on the movies/show page. 

```
//Comment Object
function Comment(json) {
  //object methods
  this.id = json.id
  this.body = json.body
  this.username = json.user.username
  } 
	//Created a comment prototype using the comment object that will save the comment attributes and return those attribute in a paragraph.
Comment.prototype.renderP = function() {    return "<p>" + this.body + " " +
"by" + " " + "<strong>" +  this.username + "</strong>" + "</p>" //this.name  }
```

The comment object has 3 object methods that assign an id, a body and the commenter's username. The comment prototype uses the comment object saves the comment attributes and returns a html paragraph. 

Check out my project [here](https://github.com/Eclecticdynasty/film-fan-rails)


