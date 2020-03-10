---
layout: post
title:      "My Sinatra Project: Flatiron Fitness"
date:       2020-03-10 16:50:22 +0000
permalink:  my_sinatra_project_flatiron_fitness
---




The second project utilizes the Sinatra framework, which provides libraries and structure to help in the development of dynamic websites or web applications.  Sinatra gives an easy way to make websites and routes using their structure.  

The requirements for the project include having users that can sign up, sign in and sign out, and the user can apply CRUD operations (Create, Read, Update, Delete) to something in the app.  The routes should be RESTful, meaning they use the URL and HTTP verb to map the route.  Examples of HTTP verbs are GET, POST, PATCH.  

When a URL is typed into the browser, the browser sends an HTTP request to the server, or in this case, the app controller.  The controller gathers info from the model which is connected to the database by ActiveRecord.  The data is then pushed from the controller to the views, and the controller sends the appropriate views (based on the browser request and HTTP verb) to the browser to be displayed as a webpage.

My project is called “Flatiron Fitness.”  Once a user signs up and logs in, the user can create a fitness goal.  The goal has a start date and an end date, a category of workout, a description, and a goal time they want to achieve.  For example, the user can set their goal for 1 week, have a 4 hour WarmUp/Stretch category, and description is Four 1 hour Yoga classes.”  The user’s Home page will show their current goal(s).  As the user has workouts, they will log their workouts with a date and the amount of time they spent.  As workouts are added that apply to the goal, they will see their progress of the goals on their homepage.  Once a goal is completed, they will be given a congratulations message.  A user can add as many goals and workouts as they like.  They can edit and delete all goals and workouts.  They can also go back to view all of their previous goals and workouts.  

The project uses Active Record which makes CRUD operations easy with the methods that come with it, such as .create and .update.  Active Record links ruby models with rows in a database by connecting SQL databases to the models.  

The project is the first full MVC (Models, Views, Controllers) app we made from scratch.  Models are the Ruby classes that hold most of the logic.  My models have methods that can display information such as the Date object the way I want it diaplayed.  There are methods to calculate the percent of the goal completed, and give status updates on the goals.  Views are what is displayed on the web page and in this project they are written in erb or embedded Ruby, which is HTML with Ruby code embedded in it. Controllers have the routes and are the connection between models and views.

The controllers have an application controller with helper methods and sets the sessions and inherits from Sinatra Base:
```
class ApplicationController < Sinatra::Base
```

The other contollers inherit from the application controller, receiving all of the methods in the ApplicationController class and inheriting sinatra from this parent class also.
```
class UserController < ApplicationController
```

My relationships are with classes User, Workout, and Goal.  A user has many workouts and many goals.  A workout belongs to the user and has many goals through workout_goals.  A goal belongs to user and has many workouts through workout_goals.  Workout_goals is the join table for the has_many_through relationship of goals and workouts.  

```
class WorkoutGoal < ActiveRecord::Base
   belongs_to :goal
   belongs_to :workout
	```

```
class Goal < ActiveRecord::Base
   has_many :workouts, through: :workout_goals
   belongs_to :user
```
 
```
class User < ActiveRecord::Base
   has_secure_password
   has_many :workouts
   has_many :goals
   validates_presence_of :name, :email, :password
   validates_uniqueness_of :email
```


```
class Workout < ActiveRecord::Base
   belongs_to :user
   has_many :goals, through: :workout_goals
 ```



My relationships are with classes User, Workout, and Goal.  A user has many workouts and many goals.  A workout belongs to the user and has many goals through workout_goals.  A goal belongs to user and has many workouts through workout_goals.  Workout_goals is the join table for the has_many_through relationship of goals and workouts, allowing goals to have many workouts and workouts to have many goals.  

The program has validations so a user cannot edit the URL to get the account information,  workout information, or goal information of a different user.  A user's password is encrypted using BCrypt.  

The project taught me a lot about routes and the MVC model.  My biggest challenge was styling the app with CSS.  I experimented with many style elements but ultimately decided to leave the styling very basic.  
