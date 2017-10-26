---
layout: post
title:      "Post Cli Data Gem"
date:       2017-10-26 15:21:25 -0400
permalink:  post_cli_data_gem
---


I thought that once my cli data gem was submitted, that would be the end of it. The experience of that project was challenging but rewarding, I wrote about it [here](http://siobhanannalise.com/2017/08/31/the_cli_data_gem_crossroads/).

Submitting my cli gem was just the beginning. My first assesment went well. My instructor asked me to change a few things and make my gem more flexible. Those requests, while minor, made me realize that I didn't have a good enough grasp on certain ruby methods and scraping in order to make those changes. My use of terminology during my assestment was also something that I wanted to work on.

I wanted to make a blog post about a few of those things. Hopefully, it'll help some of you fellow learners as well as be a great reminder/refresher for myself. 

Scraping was the most challenging part of the cli gem for me. My gem was a command line interface that gives the user a list of books to read before they die. When I scraped my data, I scraped the information for one book instead of the entire list. I used the cli data gem walkthrough video as a guideline so my scraper looked very similiar to this:

``` 
def self.scrape_woot
    doc = Nokogiri::HTML(open("https://woot.com"))

    deal = self.new
    deal.name = doc.search("h2.main-title").text.strip
    deal.price = doc.search("#todays-deal span.price").text.strip
    deal.url = doc.search("a.wantone").first.attr("href").strip
    deal.availability = true

    deal
  end
```
	
	
While this works perfectly for trying to scrape one item, it's not a great viable method for scraping a collection of data for many items. This is where iterating comes into play. *Iterating* is when you have a collection of data like an array, and you want to operate on each member of that collection.  That's what I needed to do in order for my cli gem to work best for the user. 


```
 def self.scrape_details
    doc = Nokogiri::HTML(open("http://www.powells.com/25-books-to-read-before-you-die"))

    doc.css('div.readbefore_box').each do |book_css|
      book = BestBooks::Book.new
      book.name = book_css.css('h3').text.strip
      book.author = book_css.css('.author').text.strip
      book.summary = book_css.css('p.blurb').text.strip
      book.save

    end
	```
		
Getting to this new method took quite a bit of time. Revisiting past lessons and labs helped a ton but what I gained the most help from were the study groups. Hearing the other issues and suggestions other people who were also working on their cli gem had to offer help in that many times they pointed me in the right direction of the solution I was looking for. Also, don't be afraid to make an appoinment with an instructor for help. I know it can feel like you're not sure of the right question to ask that will properly or prefectly explain what issue you're having but, ask anyway. Sometimes someone's response can lead you to asking a better question. 

Repo for my cli gem[ here](http://https://github.com/Eclecticdynasty/best_books_cli).
	

	

	



