---
layout: post
title:      "RememberRemember"
date:       2019-11-11 03:50:38 +0000
permalink:  rememberremember
---


Storing a collection of instances requires Class variables to store information as soon as it is initialized.  Decide who's responsibility it is to store information using @@all.
```class Song
 
  @@all = []
 
  attr_accessor :name
 
  def initialize(name)
    @name = name
		@@all << self
  end
end```

A class reader is the method that exposes information within a class to make that accessable outside of the class
``` def self.all
    @@all
  end
 ```
 
 A class finder is a method that streamlines finding information stored. In this example we create a method that automates the .find method on a class array
 ``` def self.find_by_name(name)
    @@all.find{|person| person.name == name}
  end```
	
	
	Abstractions:
	The above code can be improved with more abstraction. Like flipping a switch to get light in leiu of starting a fire. Abstraction of the above process will be better. The following example shows the @@all being replaced by @@people.
	```class Person
  attr_accessor :name
  @@people = []
 
  def initialize(name)
    @name = name
    # self in the initialize method is our new instance
    # self.class is Person
    # self.class.all == Person.all
    self.class.all << self
  end
 
  def self.all
    @@people
  end
 
  def self.find_by_name(name)
    self.all.find{|person| person.name == name}
  end
 
end```

Notice that in the initialize method we changed the @@all or @@person to self.class.all . This stores the initialized information in to the Person class.  so then later when we want to find something in self, we can. 

"You want to build objects that provide a semantic and obvious API, or interface. Methods that reveal what the object will do, not how it does that. Always hide the how and show the what."

custom constructors
how to simplify this:
exporting information from a spread sheet the following code could be used. 
```class Person
  attr_accessor :name, :age, :company
end
 
csv_data = "Elon Musk, 45, Tesla
Mark Zuckerberg, 32, Facebook
Martha Stewart, 74, MSL"
 
rows = csv_data.split("\n")
people = rows.collect do |row|
  data = row.split(", ")
  name = data[0]
  age = data[1]
  company = data[2]
  person = Person.new
  person.name = name
  person.age = age
  person.company = company
  person
end
people```

We should build a custom constructor to parse the incoming data with in Person class. This is why we should build a custom constructor. 
```class Person
  attr_accessor :name, :age, :company
 
  def self.new_from_csv(csv_data)
    rows = csv_data.split("\n")
    people = rows.collect do |row|
      data = row.split(", ")
      name = data[0]
      age = data[1]
      company = data[2]
 
      person = self.new # This is an important line.
      person.name = name
      person.age = age
      person.company = company
      person
    end
    people
  end
end
 
csv_data = "Elon Musk, 45, Tesla
Mark Zuckerberg, 32, Facebook
Martha Stewart, 74, MSL"
 
people = Person.new_from_csv(csv_data)
people #=> [
  #<Person @name="Elon Musk"...>,
  #<Person @name="Mark Zuckerberg"...>,
  # ...
# ]
 
new_csv_data = "Avi Flombaum, 31, Flatiron School
Payal Kadakia, 30, ClassPass"
 
people << Person.new_from_csv(new_csv_data)
people.flatten
people #=> [
#<Person @name="Elon Musk"...>,
#<Person @name="Mark Zuckerberg"...>
#<Person @name="Martha Stewart"...>,
#<Person @name="Avi Flombaum"...>,
#<Person @name="Payal Kadakia"...>
# ]```

in this example the big change of using self in a defined method to hold the parsing work will simplify our code for any incoming csv file. This is the same code with explination about what it is doing.

class Person
  attr_accessor :name, :age, :company
 
  def self.new_from_csv(csv_data)
    #Split the CSV data into an array of individual rows.
    rows = csv_data.split("\n")
    #For each row, let's collect a Person instance based on the data
    people = rows.collect do |row|
      #Split the row into 3 parts, name, age, company, at the ", "
      data = row.split(", ")
      name = data[0]
      age = data[1]
      company = data[2]
 
      #Make a new instance
      person = self.new # self refers to the Person class. This is Person.new
      #Set the properties on the person.
      person.name = name
      person.age = age
      person.company = company
      #Return the person to collect
      person
    end
    #Return the array of newly created people.
    people
  end
end

Why build a custom constructor when we could just initialize everything in to a new person object? Well what if you don't want to make a person from an incoming csv file or what if that file isn't a csv?  Initialize needs to be kept as simple as possible so it remains closed to modification. So if we need to create some new functionality later on we don't have to redo the initialize part every time but instead build a new custom constructor.


