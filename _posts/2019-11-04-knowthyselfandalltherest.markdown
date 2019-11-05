---
layout: post
title:      "KnowThySelfAndAllTheRest"
date:       2019-11-05 03:39:48 +0000
permalink:  knowthyselfandalltherest
---


Self is a way of refering to the current object and creating new information from that data.  We use the example of having a new dog with a new owner. The dog is created and then in a new method the owner's name is passed in as an argument. As a nice to have, ruby allows us to refer to the dog object as self 
```adopted(fido, "Sophie")
 
# now we can ask Fido who his owner is:
 
fido.owner
  => "Sophie"
However, the beauty of object-oriented programming is that we can encapsulate, or wrap up, attributes and behaviors into one object. Instead of writing a method that is not associated to any particular object and that takes in certain objects as arguments, we can simply teach our Dog instances how to get adopted.

Let's refactor our code above into an instance method on the Dog class.

class Dog
 
  attr_accessor :name, :owner
 
  def initialize(name)
    @name = name
  end
 
  def bark
    "Woof!"
  end
 
  def get_adopted(owner_name)
    self.owner = owner_name
  end
 
end```

In the sentences OOp Lab they discuss monkey patching.  What is Monkey Patching? well according to the lab definition it is when you program a ruby method that interupts or modifies a core class. A core class like String for example.  "Monkey patching is the practice of adding methods to or altering Ruby's core classes. Monkey patching is dangerous! What if, for example, you decide to monkey patch Ruby's String class to produce a quick-fix that shortens a certain section of code in your program. " 

``` require 'pry'

class String
  def sentence?
    if self.end_with?(".")
      return true
    else
      return false
    end
  end

  def question?
    if self.end_with?("?")
      return true
    else
      return false
    end
  end

  def exclamation?
    if self.end_with?("!")
      return true
    else
      return false
    end
  end

  def count_sentences
    num_sentences = self.split(/[.?!]+\s/)
    num_sentences.length
    
  end
end``` 

