---
layout: post
---
<img src="/images/fulls/reddit.jpg" class="fit image"> Lightweight case study into the development of a Reddit clone using Ruby on Rails.

Creating and committing to a development side project might be one of the most difficult things to do. With so many options, and a seemingly endless level of complexity, picking an idea and sticking to it is a skill set in and of itself. Usually I tend to start a side project with the sole intent of learning a new skill set and building on it, and by chance I recently picked up developing with Ruby on Rails. To solidify my knowledge I decided to dig deeper by building a side project to showcase and implement techniques I have picked up from my readings. Ruby on Rails is a fairly comprehensive web application framework based on a Model-View-Controller platform and provides a nice template for setting up databases, web pages, and web services. So with a few months of education on Ruby and its features I decided to list out a few of my frequently visited websites with the intention of replicating its features in RoR.

Modeling a Reddit Clone

I decided to use Reddit as a foundation since it is a site I visit regularly, developing its core functionality on rails would not only provide a good learning opportunity, but it would also provide me with deeper appreciation for the site itself. Reddit is a social news aggregation site, where community members can submit text posts or direct links. Registered users can cast a vote on each post for or against, and the submissions with the most positive votes gain priority to the top of the site. 

The first step of creating this application required documenting the core functionality of the site I wanted to create. Listed below are the general core function I deemed a necessity for a user to use my site and deduce that it is a copy of Reddit. 

1.	User login 
2.	Creating a Topic
3.	Creating a Post
4.	Creating a Comment
5.	Voting system on Posts
6.	Voting system on Comments
7.	User Profile
8.	Labeling Posts by subject topic


Implementation

Using generic Bootstrap assets, I was able to quickly mock up the general structure of the web pages and views I intended to use. Creating the views as a form of functional wireframing helped organize the workflow a bit better and proved to be a better visual aid compared to quick physical sketches. Models and Migrations were the first order of business with my reddit clone, since establishing what data types need to be created is imperative to the design and functionality of the site.  

`$ rails generate model Post title:string body:text `

`$ rails generate model Comment body:text post:references `

A great learning opportunity during this process was tackling rails based Object Relational Mapping.  Within Reddit, user comments are associated to community posts. Rails built in conventions made making associations fairly straightforward. 

Developing the sites controllers were the next order of business, this proved to be the meat and potatoes of the process. Controllers manage the CRUD functionality and moved all of the pieces into place from the models to the view. A thin view, heavy controller and middleweight model proved to be a fairly good implementation strategy when creating a bunch of moving pieces. 

Creating the functionality of the site on a high level opened a Pandora’s box as to design oriented decisions I did not consider during the early stages of the project. A lesson learned early on during this process was to drill down on every design choice and explore all possible options from those choices. For example, creating a list of core functions as I did above was a decent reference, however something like this would have served a much better template:
 
1.	User Login
*   Valid / Invalid Login logic
*   Creating a User Session
2.	Creating a Topic
*	Posts are associated to Topic
*	A Topic has Many Posts
3.	Creating a Post
*	Posts belong to a Topic
*	Post has many Comments
*	Post belongs to a User
4.	Creating a Comment
*	Comment belongs to User
*	Comment belongs to Post
5.	Voting system on Posts
6.	Voting system on Comments
7.	User Profile
*	Display User information
*	Display User interactions with Post and Comments
8.	Labeling Posts by subject topic
*	Polymorphic association to Posts

Reddit’s time decay algorithm 

Possibly the most interesting feature of Reddit is its ability to organize community posts by vote popularity and self-regulating new popular posts above older popular posts. As a post ages, it slowly falls off from the front page to give way to newer posts with relative high voting averages. To replicate this functionality I implemented a fairly simple time decay method that calculated the age of the post relative to Unix epoch and added it to the votes points. This way new posts have priority over older posts and additionally new posts with higher rank would have priority over older posts with similar rank. 

```ruby
   def update_rank
     age_in_days = (created_at - Time.new(1970,1,1)) / 1.day.seconds
     new_rank = points + age_in_days
     update_attribute(:rank, new_rank)
   end
```


Test Driven Development

One of the largest take always I gained from jumping on this project was the importance of Test Driven Development. Instead of generally hacking away code until something works as intended -  writing out tests solidifies not only that the code functions as intended, but it documents with proof that your code does not break if it is used incorrectly. Developing tests admittedly took a few tries initially, and was a bit of a struggle to wrap my head around, however sticking to the TDD guidelines helped me become a better developer since it requires more methodical approach to developing. Although I wrote my tests after development to confirm code worked as intended – I am slowly transitioning to developing tests before writing production code in efforts to create a systematic list of the applications functions. I believe creating test before developing will help in understanding the design architecture of the application better, and provide a good reference to what functions an application needs to produce to solve the test problems. 

TL;DR

In summation, creating a Reddit clone proved to be a deeply rewarding experience – It opened the door to learning Ruby on Rails and provided me the opportunity to develop a project as the lead architect, designer, developer and administrator. I intend on cleaning up the interface a bit, since I realized halfway during this process that generic bootstrap assets do not convey Reddit’s minimalist style. All in all I am extremely satisfied by the end product, and look forward to refactoring the application from here on.  Feel free to fork [@github.](https://github.com/Jigesh-Parekh/bloccit)
