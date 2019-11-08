---
layout: post
title:      "PrivateMethods"
date:       2019-11-08 01:32:11 +0000
permalink:  privatemethods
---

Building Classes and Methods we want .distinguish between all the different types. 
An instance method is a method that is called on an instance of an object. Like this one below: 
```class Bartender
  attr_accessor :name
 
  def initialize(name)
    @name = name
  end
 
  def intro
    "Hello, my name is #{name}!"
  end
end
 
phil = Bartender.new("Phil")
phil.intro
#=> "Hello, my name is Phil!"```

A class method is a method that is called on a class itself. Such as this example that has a class method that keeps track of how many instances bartenders there are.
```class Bartender
  attr_accessor :name
 
  BARTENDERS = []
 
  def initialize(name)
    @name = name
    BARTENDERS << self
  end
 
  def self.all
    BARTENDERS
  end
 
  def intro
    "Hello, my name is #{name}!"
  end
end```

Public Methods  are methods that are explicitly recieved by an instance. 
Private Methods can not be called explicity by a reciever. The reciever for a private method is always self. Private Methods basically allow for functions that only pretain to that object or instance. Private methods help to keep code organized in little pods so that a program runs efficiantly. 

Here is an example of how to structure private and public methods:
```class Bartender
  attr_accessor :name
 
  BARTENDERS = []
 
  def initialize(name)
    @name = name
    BARTENDERS << self
  end
 
  def self.all
    BARTENDERS
  end
 
  def intro
    "Hello, my name is #{name}!"
  end
 
  def make_drink
    @cocktail_ingredients = []
    choose_liquor
    choose_mixer
    choose_garnish
    return "Here is your drink. It contains #{@cocktail_ingredients}"
  end
 
  private
 
  def choose_liquor
    @cocktail_ingredients.push("whiskey")
  end
 
  def choose_mixer
    @cocktail_ingredients.push("vermouth")
  end
 
  def choose_garnish
    @cocktail_ingredients.push("olives")
  end
 
end```

Notice that a bartender object will not be able to call the choose_liquor method. it is not available for that. 

