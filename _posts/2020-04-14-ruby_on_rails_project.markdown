---
layout: post
title:      "Ruby on Rails Project"
date:       2020-04-14 19:47:25 +0000
permalink:  ruby_on_rails_project
---




My Ruby on Rails project is an idea where people post fun locations or events in their town, and other people can search places they want to go and see the events posted by people, add them to their list of events, and rate them. 
 Rails is a framework in the Ruby language that streamlines the development of web applications.  Rails does a lot of the work for the developer.  For example, Rails can generate parts of the MVC model with simple commands in the terminal.

```
rails generate resource Artist name:string bio:text 
```

Resource generator creates a model, database table, controller, views folders and CRUD routes based on the information given after declaring ‘generate resource’, with the model/controller name starting in a capital letter, and the columns for the database table listed as name_of_column:datatype.


```
rails generate model Artist name:string bio:text 
```
The model generator creates a model and the associated database and routes with the same syntax, with the model being the Artist in this example.


```
rails generate controller artist create update show 
```
The controller generator creates the controller routes and views.

And a scaffold generator generates a migration file for the database, the controller, the model, full set of RESTful routes, templates for controller actions, view templates for each of the controller actions among many other things.

While this can be useful and time-saving, I did my application without any generators because I wanted to build it out on my own.

The project had many requirements to meet, including making certain associations between the database tables using Active Record in the models.  My associations are 
 Events belong to the user who created it (so only users who created the events can edit an event) and events has many users through a join table of UserEvents.  Events have many feedbacks where they can rate and comment on an event.  Feedback belongs to user and events.  This is where my nested route new form came in.  UserEvents belongs to user and event, and this is the join table allowing users to have many events.  User has many events, many user_events, and added_events (which is an alias to differentiate events a user created themselves and events added that were created by a different user), and a user has many feedbacks (or comments/ratings on events).

The alias association was created using this code in the User model:
```has_many :added_events, through: :user_events, source: "event"```

Along with meeting the Flatiron school requirements for the project, I added the GoogleMaps gem for rails and Geocoder gem for rails to include maps to my pages.  Individual events show a static map of where the event is located.  When searching a location from the home page to see what events exist for that location, a dynamic map is shown with markers for each location.  

The login and logout have an option to login through Facebook or Github, using the Omniauth gem.  

All of these API keys are saved using the dotenv gem, which hides them from being saved to github.  

Like my last project, styling was a challenge.  This time I used TailwindCSS to do some styling, though I still kept the sytling pretty basic.  

Overall, I learned a lot making this project and I am excited to continue my journey learning how to code.


