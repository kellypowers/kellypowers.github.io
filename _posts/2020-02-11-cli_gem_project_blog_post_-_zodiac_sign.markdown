---
layout: post
title:      "CLI Gem Project Blog Post - Zodiac Sign"
date:       2020-02-11 17:30:14 +0000
permalink:  cli_gem_project_blog_post_-_zodiac_sign
---




The Flatiron School’s full-time online bootcamp gives the opportunity to create your own project  at the end of each section in order to showcase the things you have learned.  The first section was on Procedural Ruby and Object Oriented Ruby.  My project takes the information displayed on https://zodiacal.herokuapp.com/api and gathers the data to be shown in a Command Line Interface program.  

Before beginning to code I mapped out my idea on paper of how I imagined the flow of the program.  I wanted to have the program ask for the user’s date of birth and use that to look up and return the relevant zodiac sign.  Then, the program would give a menu of options on what the user wants to know about the zodiac sign.  This would include the basic things such as the dates for the sign, the element associated with it, and the traits the signs are typically known for in astrology.    

The first step to writing the program was twofold: creating a class where each instance would be a zodiac sign, and gathering the data from the API into a format that I could manipulate to pass to the zodiac class so that each trait would be it’s own instance method created upon initialization.  Initializing an instance of the Zodiac class with an unknown set of attributes is something I had done before in the labs.  It is called mass assignment and is done using this code:

```
def initialize(attributes)
attributes.each {|key, value| self.send((“#{key}=”), value)}
end
```

This sets the initialization of a class with a hash of attributes where the key is the method and the value is the return value of the method.  

The API data is in JSON format and already almost in hash form for the code above to use.  I had not scraped API data before in this way, so it took some googling and trial and error before I was able to extract the data in the form I needed.

Starting the program with the begin method instantly creates all 12 Zodiac class instances using the scraper and the mass assignment of the instance methods.  The program asks for the user’s date of birth and the response is passed to the check_birthday method which checks that the date of birth is in the correct format.  The date of birth is passed to the Ruby Date object.  Since the Date object does not allow for a hyphen in the date, the check_birthday method changes any hyphen to a backslash before passing it to the Date object using the .gsub method.  The check_birthday method checks that the date is a valid length and turns the date into the month and date into the format “January 29” using the class constant MONTHNAMES.  The purpose of asking the user if this is the date they wanted is because the Date object may turn an input of “111” into “April 20” and I want the user to see their entry and verify it is correct before giving them their zodiac sign. 

After the user confirms their date of birth, if the date found between the dates for each zodiac sign, taken from the zodiac API.  In creating the method that takes the user’s birthday and returns the zodiac sign, it was necessary to make an exception for Capricorn because those dates include the beginning of the year and the end of the year.  If the date is found between the dates of a zodiac sign, the zodiac sign is given to the user along with a list of items they can look at relevant to that sign.  There were many different traits for each sign; good traits, bad traits, mental traits and physical traits.  I decided to combine all the good, bad, and mental traits into one instance method for the zodiac class.  
  
The zodiac instance is passed into the zodiac_info method which gives a menu option of selected methods and asks the user what they want to know.  Their input is used to select the method, which is then passed to the zodiac instance to give the value.  The values of the zodiac instance methods were often in array format, so I made a method that displayed the results to start with a capital letter and printed each of the array’s values on a new line.  I added an exception for the “Famous People” method because the .capitalize method gave the names of each person only a capital first word and not a capital middle initial or last name.  

After looking at the selected information, the user is asked if they want to look at another characteristic of the same zodiac sign, if they want to look at a different zodiac sign, or they want to exit.  Selecting a different zodiac sign would create a new instance of the zodiac class, and the user can look through those characteristics and select as many signs as they want and view their characteristics.  

An issue I had was passing the current zodiac instance to each method and looping through the menu options so the zodiac instance did not change.  To do this, I made the zodiac variable an instance variable in the CommandLineInterface class and I refactored my methods to be called in a more straightforward way, rather than wrapping back around to several different functions.

The CLI class has the majority of the code.  I added helper functions to make the data look nicer and cut down repetition. Adding the colorize gem made the menu options appear in a different color in order to stand out more.  

The first draft of the program worked in the same way but was much longer and more complicated.  Refactoring the code several times cut the program size down and eliminated the hard coded elements.  Initially I did not use the Date object, but instead had hardcoded a hash of the zodiac signs and dates.  Also, I originally hard-coded the methods to be passed to the zodiac sign into an array which would be called upon using the user’s selection.  Taking out the hard-coded elements makes the code look nicer and more professional, and it also taught me to look at problems different ways until a better solution was found.




