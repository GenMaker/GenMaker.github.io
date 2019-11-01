---
layout: post
title:      "MyDomainIsAll "
date:       2019-11-01 03:28:03 +0000
permalink:  mydomainisall
---



What is a Domain. It is important concept in OOP. If classes are templates for objects, ie classes hold properties for objects, then each instance of that that class is an object and then we program methods with that object. The metaphore used in the lab is the idea of a car factory. That our program will be able to handle the making of new cars but also inventory, paint jobs- representing not just a single car but an entire environment. 

The lab to practice this concept is a school. our program will 
1. create a new school
2. each school has a rooster
3. add a student to that roster
    it is at this step we learn more about how to add new information in a hash utilizing the key and value. 
		To add a student to the roster we will have the student name and grade
		if we have an array
		```hash = {}```
		and then we try to push a new key and value at the same time it will raise an error
		```hash["new_key"] << "new_value_for_value_array"
 => NoMethodError: undefined method `<<' for nil:NilClass```
 We have to create the new key first and then we can submit a new value in that key
 ```hash["new_key"] = []
hash["new_key"] << "new_value_for_value_array"
 
hash
 => {"new_key"=>["new_value_for_value_array"]} ```
 
 The resulting program for adding values to a hash looks like :
 ```  def add_student(name, grade)
    @student_name = name
    @grade = grade
  #binding.pry
    if @roster.include?(grade) == false
      @roster[grade] = []
    end
      @roster[grade] << name
  end```
4. Checking if there is already a grade. Above notice that we add an if statement that checks to see if a key (grade) already exists in the  hash. This way we don't over ride information that is already there.
5. finished program that sorts students by grade.
```require "pry"
# code here!
class School
  def initialize (school_name)
    @school_name = school_name
    @roster = {}
  end

  def roster
  @roster
  end

  def add_student(name, grade)
    @student_name = name
    @grade = grade
  #binding.pry
    if @roster.include?(grade) == false
      @roster[grade] = []
    end
      @roster[grade] << name
  end

  def grade (number)
    @roster[number]
  end

  def sort
<<<<<<< HEAD
    @roster.each do |grade, name|
      @roster[grade]= name.sort
    end
  end
=======

    @roster.each @roster do |grade, name|
      @roster[grade]= name.sort
    end

  end

>>>>>>> 88da4a792aa4d377b7969db81dc97fad846fb20d
end
```

