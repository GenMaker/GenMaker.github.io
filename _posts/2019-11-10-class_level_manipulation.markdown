---
layout: post
title:      "class level manipulation"
date:       2019-11-10 23:06:30 -0500
permalink:  class_level_manipulation
---


Here are some more coding samples showing how manipulating class level data can  make code more simple and clean:
This code creates a person from a list and prints the out:

```class Person
  attr_accessor :name
  @@all = []
  def self.all
    @@all
  end
 
  def self.create(name)
    person = self.new
    person.name = name
    @@all << person
  end
 
  def self.print_all
    self.all.each{|person| puts "#{person.name}"}
  end
end
 
Person.create("Ada Lovelace")
Person.create("Grace Hopper")
 
Person.print_all```


class operators can help to modifiy every thing: like a list of names coming to you with all lower case letters. You might make this to adjust that:
```class Person
  attr_accessor :name
  @@all = []
  def self.all
    @@all
  end
 
  def initialize(name)
    @name = name
    @@all << self
  end
 
  def normalize_name
    self.name.split(" ").collect{|w| w.capitalize}.join(" ")
  end
 
  def self.normalize_names
    self.all.each do |person|
      person.name = person.normalize_name
    end
  end
end```




