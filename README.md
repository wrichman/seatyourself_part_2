# Seat Yourself Tutorial

# Plan Your Project
**Read before beginning!**

Writing code is only one part of software development. Long before we sit down and write any code, you will need to plan out what you'll be doing.

## Step 1

We'll want to:
* Decide what problems we are trying to solve
* Think about who will be using our application
* Decide what our goals are, and what "done" will look like
* Understand our constraints, e.g. when the project must be completed, what the budget is, etc.
* Decide on what features are absolutely necessary versus optional

In the case of Seat Yourself, we have 3 days and the weekend, so it is your job to assess what level of detail you would like to go into.

A good philosophy is, after understanding the problem well, to write the least amount of code to meet a given set of requirements and once those requirements are met, ask if the product owner would like to add more functionality. This is a much more focused approach than guessing what functionality they might want in the future. You would be surprised at how much information is lost in translation from one person to the next.


### User Stories

At this stage, a useful tool is to write user stories. Here are some user stories we might write for Seat Yourself. 

1. As a visitor, I want to see a directory of the restaurants available.
2. As a visitor, when I click on a restaurant, I want to be able to see:
  * address
  * neighbourhood
  * price range
  * summary
  * menu
  * a list of available timeslots
3. As a visitor, I want to sign up for a customer account so that I can make reservations online.
4. As a customer, I want to be able to make a reservation online.
5. As a customer, I want to receive loyalty points when I make a reservation.
6. As a customer, I want to see my loyalty points in my account profile.
7. As a customer, I want to receive an email confirmation after I've made a reservation.
9. As the restaurant owner, I want to see the list of the weeks reservations.
10. As the restaurant owner, I want to see my customer list with how many points each person has and how much they have spent online.
11. As a visitor, I would like to be able to view restaurants based on their cuisine category (e.g. Italian). This can be down with a drop-down menu using collection_select.
12. A restaurant can only be open from 11am - 8pm, 7 days a week.
13. A restaurant can only hold 100 people in any given time slot.
14. A reservation can be for a party of 2 to 20 people.


## Step 2

Now that we have a good understanding to the above questions, we can refine our plans and make them more concrete. Here we want to
* create mockups
* draw out what entities (models in Rails) we will need and how they will relate to each other (associations in Rails)

### Mockups

Once we understand the general picture of the application, lets create static web pages to guide the construction of our application. Below is a passage from the blog article [A Comprehensive Guide to Mockups in Web Design](http://psd.fanextra.com/articles/a-comprehensive-guide-to-mockups-in-web-design/):

A "Mockup" is a refinement of the conceptual user interface design and results in a more or less realistic, though static simulation of the user interface. You may build on the wireframe with dummy text, color, graphics and polish, and may adjust layout slightly but stays within the general guide of the wireframe.

* **A mockup lets you know which information goes where.** – You know which information goes where before you start writing the functional analysis or request for offer.
* **Can be used for design implementation.** – Which means it’s possible to test your layout concept and trend before you’ve written a single word of code. Changes in the concept are easily and cheaply fixed.
* **Attention to detail.** – About functionality and make sure you have visitor’s perspective. You can gauge which functions work better than others, and which conflict with overall usability
* **Flexibility.** – Changes, delete or even add more points about your ideas and concept are easily.
* **Valuable service.** – If you can give potential clients this mockup as a free service, it means you can provide more value that other designers/developers out there.
* **As part of the proposal.** – If the client is huge, lucrative, prestigious, and interesting then perhaps you could invest some time in winning this job by providing a mockup. Be careful when providing mockups that you are sure to have them sign a legal document stating that they cannot use any part of your concept or design without paying for it. Sometimes unscrupulous clients will have you do a mock up and then use it without hiring you!
* **Remember that your job depends on this phase.** – Clients will appreciate your work. This is important how you can often win a client’s approval through your mockup design. If your client was happy for what you’ve done with mockup design, the next phase of this job will be very easy for you

Here are a couple of example mockups to get you started:

Original Twitter Concept

![Original Twitter Concept](http://webdesignledger.com/wp-content/uploads/2010/05/sketched_wireframes_18.jpg)

Vimeo Profile Page Idea

![Vimeo Profile Page Idea](http://webdesignledger.com/wp-content/uploads/2010/05/sketched_wireframes_7.jpg)

5 Years of Firefox

![5 Years of Firefox](http://webdesignledger.com/wp-content/uploads/2010/05/sketched_wireframes_2.jpg)

#### Make Your Mockups

Create mockups for Seat Yourself based on the user stories and translate them into static HTML pages that _look_ like a fully functioning application.

### Entity-relationship (ER) Modeling

This is a fancy way of saying that you need to decide what entities (models in Rails) you will want and how they will relate to each other (associations in Rails). An ER model is an abstract way of describing a database. Diagrams created to design these entities and relationships are called entity–relationship diagrams or ER diagrams. [Wikipedia](http://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model)

![Example ER Model](http://www.fancybread.com/blog/images//trivia.gif)

Above is an ER diagram for a trivia game data model, which contains the following entities: User, Theme, Category, Game, Question, Answer and Response. This is a simple data model with several one-to-many relationships and no many-to-many relationships.

Briefly, a Game has a parent User and Theme. A Question has a parent Game and Category. An Answer has a parent Question. And a Response has a parent User, Question and Answer.There's nothing too complex about this data model, so I'll focus on the conventions used to name the table primary and foreign key attributes. Each table has a PK named simply "Id" and each foreign key is prefaced by the parent entity name and "Id". For example, the Game entity has foreign key attributes "ThemeId" and "UserId".

This passage was written by Paul Marcotte from the blog article [Scaffolding a Generic Admint Part 2 - The Data Model](http://www.fancybread.com/blog/post.cfm/scaffolding-a-generic-admin-part-2-the-data-model).

#### Model Your Entities

Using the above as an example, first we'll make a diagram to represent our models. At a minimum, the models we will need are:
* User
* Restaurant
* Reservation
* Category

## Step 3

Now that you have a good idea of what you're going to build, you need to decide the order in which you will build all the parts. How do you do that?
* Think about dependencies. Creating a Reservation is _dependent_ on the existence of a Restaurant and a User. Therefore, you will first create the Restaurant and User models, and _then_ add the Reservations model
* A good tactic is to plan your application in steps, such that each step is a minimally useful website. So if you create a Restaurant model, then create a RestaurantController and set up the CRUD (7 RESTful actions) so that you can add and view Restaurants _before_ you create the User model. You don't want to create two models, before you have one model that does anything.

# Pry

Given the difficulty of this application we're going to need to improve our problem solving and debugging skills. An extremely useful tool for the latter is called **Pry**.

Pry is a powerful alternative to the standard IRB shell for Ruby. It features syntax highlighting, runtime invocation and source and documentation browsing. To learn more about it,  [Pry Wiki](https://github.com/pry/pry/wiki)

#### Source and Documentation Browsing

We install the gem by running the following command:

```bash
$ gem install pry
```

We start our pry session:

```bash
$ pry
```

We can view what commands are available while using pry:

```bash
pry(main)> help
```

We'll have to install an add on called "pry-doc", which provides access to Ruby core documentation and source code within Pry:

```bash
$ gem install pry-doc
```

You can check out anything you would find in the Ruby docs in your terminal. Try the following command:

```bash
pry(main)> show-doc Array
```

It should output a brief explanation of the Array class.

![Pry Show-doc Array](http://i.imgur.com/tZwKCLW.png)

You can also view documentation for specific methods:

```bash
pry(main)> show-doc Array#each
```

![Pry show-doc Array#each](http://i.imgur.com/nvIGZBb.png)

## Runtime Invocation Use Cases

Pry can be invoked in the middle of a running program. It opens a Pry session at the point it's called and makes all program state at that point available. It can be invoked on any object using the `my_object.pry` syntax or on the current binding (or any binding) using `binding.pry`. The Pry session will then begin within the scope of the object (or binding). When the session ends the program continues with any modifications you made to it.

There are a variety of use cases for runtime invocation of a Pry session, some include:

### Developer Console:

Having Pry run in its own thread giving you interactive access to your application while it is running.

### Debugging:

Inserting a binding.pry at the point in your program you want to debug, making all state at that point available for interactive inspection (including locals).

### REPL-oriented development and hot-patching:

Modifying the program while it is running to provide new features.

### Try it Yourself

Now let's get started with a couple Pry commands. We'll be using `show-input`, `amend-line N [replacement code]` and `binding.pry`. Here's an example of using `show-input` and `bind.pry` in combination.

```bash
pry(main)> def learning_pry
pry(main)>*   puts "Learning pry was an invaluable experience"
pry(main)>*   puts "Now I am set to conquer the world"
pry(main)>* show-input
1: def learning_pry
2:   puts "Learning pry was an valuable experience"
3:   puts "Now I am set to conquer the world"
pry(main)>*   amend-line 2 puts "Learning pry was an invaluable experience"
1: def learning_pry
2:   puts "Learning pry was an invaluable experience"
3:   puts "Now I am set to conquer the world"
pry(main)>*   show-input
1: def learning_pry
2:   puts "Learning pry was an invaluable experience"
3:   puts "Now I am set to conquer the world"
pry(main)>* end  
```

Last and most importantly, we're going to learn how to use `binding.pry` to debug our Ruby programs. Create a ruby script with the following.

**`ruby_test.rb**
```ruby
def say_hello
  binding.pry
  puts '1', '2'
  puts '3', '4'
end

say_hello
```

In your terminal, type the following:

```bash
$ pry
pry(main)> load 'ruby_test.rb'
pry(main)> play -l 3
```

This shows how you can stop programs at any point and run specific lines of code in your program to better understand how it works.

# Callbacks

Callbacks are methods that get called at certain moments of an object’s life cycle. With callbacks it’s possible to write code that will run whenever an ActiveRecord object is created, saved, updated, deleted, validated, or loaded from the database.[RG Active Record Validations and Callbacks: 9 Callbacks Overview](http://guides.rubyonrails.org/v3.1.3/active_record_validations_callbacks.html#callbacks-overview)

An example of how you could use callbacks in your application is shown below.

**`app/models/reservation.rb`**
```ruby
class Reservation < ActiveRecord::Base
.
.
.  
  after_create :add_user_points
  after_destroy :remove_user_points
  
  def remove_user_points
    self.user.points -= self.party_size * 10
    self.user.save
  end
  
  def add_user_points
    # self.user.update_attributes(points: self.user.points + self.party_size * 10)
    # self.user.points = self.user.points + self.party_size * 10
    self.user.points += self.party_size * 10
    self.user.save
  end
  
  validate :less_than_max_occupancy
  
  def less_than_max_occupancy
    other_people = Reservation.where(:booked_for => self.booked_for, :hour => self.hour).sum(:party_size)
    
    if other_people + self.party_size > 30
      errors.add(:base, "Sorry, too many people!")
    end
  end
  
end
```

# Testing Your Rails App

We realize that you have learned a large number of new concepts in a short amount of time and are trying to tackle a difficult problem with no clearly defined solution. Ideally this problem would be solved through a process of Test Driven Development, but we think it is more important to understand the basics of the application before you get comfortable with the TDD workflow. We will use a **Verification Testing** methodology to check that the application functions as expected.

## Complete the following

We would like you to now be able to lean against your tests when refactoring your code, but in order to do so you will need to write **at least** the following tests.

## Setting up your factories.

1. Create a factory for a category
2. Create a factory for a user
3. Create a factory for a restaurant, if it belongs to anything, please make that association in your factory
4. Create a factory for a reservation, if it belongs to anything, please make that association in your factory

## Reservation Tests

1. When a restaurant is full, it should not be available for reservations
2. A user should not be able to make a reservation outside of operating hours

## User Tests

1. A user's name is required
2. A user's email is required
3. A user's password and password_confirmation are required
4. A user's password_confirmation must match password
5. An unsafe user password should not authenticate
6. A safe user password should authenticate
7. Two users cannot have the same email

## Category Tests

1. A category should have a name

## Restaurant Tests

1. A restaurant must have a name
2. A restaurant must have an address
3. A restaurant must have a phone number
4. A restaurant must have a picture
5. A restaurant must have a description
6. A restaurant must belong to a category
7. A restaurant must not be able to accept more people than it's capacity
