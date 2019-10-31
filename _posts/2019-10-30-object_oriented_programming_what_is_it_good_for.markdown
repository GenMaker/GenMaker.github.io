---
layout: post
title:      "Object Oriented Programming: What is it good for?"
date:       2019-10-30 23:05:14 -0400
permalink:  object_oriented_programming_what_is_it_good_for
---


Object Oriented Programming is hard.  That might sound seriously ridiculous and stupid to some and perhaps a 'duh' idot statement of the obvious to others so here is my attempt to summarize it for myself. 

In real life there is stuff (insert noun here) and this stuff can things that have properties that interact with other stuff with properties. So how do we organize it all and get specific results with this stuff?  Some results might be to make methods do something, save something, look somewhere and get some information to give back to a user.   Let's get specific.

1. Define a Class .  
 Classes are a way to group types of actions for specific type of object.  To create one is called Defining a class. In the example below this is it's simplest way you can create new objects in the new class in Ruby
 ```
 #start a new class
class Dog
end

#instantiate new dogs
fido = Dog.new
snoopy = Dog.new
lassie = Dog.new```

2. Now we can make these objects do something. We can store information for each object or return some value. Here we have dogs that can bark and sit.

```
class Dog
  def bark
    puts "Woof!"
  end

  def sit
    puts "The Dog is sitting"
  end

end

fido.= Dog.new
fido.bark
=> "Woof"
fido.sit
=> "The Dog is sitting."
```

3. Require Reletive: In the learn IDE we program our work in .rb files but how do tests work on them?  The test file spec uses the require_reletive to link with our files so the test file will have access when it runs.
```require_relative '../lib/dog'
require_relative '../lib/person'

RSpec.configure do |config|
  config.order = :default
end
```
4. Setting and Getting.  When we create a new object there are some things that need to happen. There should be a method that gives our object a name (Setting)aka name=, and makes sure that name is == to that object (getting) . So there are tools to help us do this efficiently. We don't have to write these two methods over and over again for everything we create. This is called attr_accessor and attr_reader.

```class Dog
  def name=(dog_name)
    this_dogs_name = dog_name
  end
 
  def name
    this_dogs_name
  end
end```

Taken from the learn readme:
"Here we've defined two instance methods, the name=, or "name equals" method, and the name method. The first method takes in an argument of a dog's name and sets that argument equal to a variable, this_dogs_name. The second method is responsible for reporting, or reading the name. The methods act as mechanisms to expose data from inside of the object to the outside world."

```lassie = Dog.new
lassie.name=("Lassie")
 
lassie.name #=> "Lassie"```

5. instance variables vs local variables
Local variable such as ```x = 10``` only have a local scope. This means that other methods in our class does not have access to it or knows that it exhists with out passing it directly thorugh arguments.  So when we want to make changes or set new values to these variables we need to change it into instance variables.  This means that the variable will follow a particular instance around any where in the Class. we do this by adding a @ infront of the property.
```class Dog
 
  def name=(dogs_name)
    @this_dogs_name = dogs_name
  end
 
  def name
    @this_dogs_name
  end
end
 
lassie = Dog.new
lassie.name = "Lassie"
 
puts lassie.name
 ```

6. setter and getter
So how do you know what your method needs to set and/or  get?  In this example below a person object has a name. Depending on what information you need, to do the thing you want to do, those values have to be brought in from somewhere else.  We label the data with descriptive titles - like name, age, etc
```class Person
  def initialize(name)
    @name = name
  end
 
  def name
    @name
  end
end
 
kanye = Person.new("Kanye")
kanye.name #=> "Kanye"```

7. Initializing:
This method is required at the begining to bring values into your class in order to manipulate.
If , like in this example someone wants to change their name then you need to make a setter method.
```class Person
 
  def initialize(name)
    @name = name
  end
 
  def name
    @name
  end
 
  def name=(new_name)
    @name = new_name
  end
 
end```


8. Responsibility: 
In OOP you have to keep in mind whose job it is to keep track of information in the Basics lab we go step by step to program a book record keeping program that lets us practice the idea of information responsibility.
 To set things up we intitalize a book class. 
 ```# book.rb
 
class Book
end```
The tests in the code along suggest that there is a value being passed in that is not accounted for in our book class so we should initialize this value. Based on the spec test file we are assuming the value is a title of the book.
```class Book
 
  def initialize(title)
  end
 
end```

9. When things happen: 
The spec goes on to show that the value of our book returns nil. Even though we initialized the title and even built a method called title. we haven't actually assigned that information to anything. So when or where should this happen?  When it initializes! your right. It's like when you buy groceries and it automatically goes in the fridge where it belongs.
```# book.rb
 
class Book
 
  def initialize(title)
    @title = title
  end
 
  def title
  end
 
end```

10. property= 
Ruby allows us to use the syntax of ```property=``` within a method to assign values. So when spec test shows that our book doesn't have an author we can decide to use the ```property =``` to allow this value to be set. This is called a setter method for that reason. A user should be able to enter ```book.author = JK Rowling``` so to set this value. 
```# book.rb
 
class Book
 
  def initialize(title)
    @title = title
  end
 
  def title
    @title
  end
 
  def author=(author)
    @author = author
  end
 
end```


11. Don't forget to get
 so now there is a setter for the author we need to also include a getter method. the setter and getter often come in pairs. 
 ```# book.rb
 
class Book
 
  def initialize(title)
    @title = title
  end
 
  def title
    @title
  end
 
  def author=(author)
    @author = author
  end
 
  def author
    @author
  end
 
end```

12. Not just for properties- Oh behave yourself:  
OOp lets us have classes with properties and behaviors like this turn page behavior.
``` 
# book.rb
 
class Book
  def initialize(title)
    @title = title
  end
 
  def title
    @title
  end
 
  def author=(author)
    @author = author
  end
 
  def author
    @author
  end
 
  def page_count=(num)
    @page_count = num
  end
 
  def page_count
    @page_count
  end
 
  def genre=(genre)
    @genre = genre
  end
 
  def genre
    @genre
  end
 
  def turn_page
    puts "Flipping the page...wow, you read fast!"
  end
 
end```

13. Not so fast: Make it simple 

so the above code is looking Long and there is an aweful lot of setting and getting happening. We can use the Attr_accessor to simplify that.
```# book.rb
 
class Book
  attr_accessor :author, :page_count, :genre
 
  def initialize(title)
    @title = title
  end
 
  def title
    @title
  end
 
  def turn_page
    puts "Flipping the page...wow, you read fast!"
  end
 
end```





