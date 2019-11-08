---
layout: post
title:      "ClassMethods and Variables"
date:       2019-11-08 01:19:12 +0000
permalink:  classmethods_and_variables
---


Remember that an object is a collection of data and logic, and that a class is a way to make instances of an object that can enact behaviors.  Objects can have data and attibutes and so can Classes. Classes then are essentially objects by definition.   In the unit they use the concept of Albums
```class Album
 
  def release_date=(date)
    @release_date = date
  end
 
  def release_date
    @release_date
  end
end```

If you wanted to count how many albums you had, we would need a class variable to keep track of that. When adding new features or functionality one needs to ask "Who is responsible?" 

" Right now, our program is pretty simple. We have an Album class and we have album instances. So, is it the responsibility of an individual album to keep a count of all of the other albums? Or is it the responsibility of the Album class, which actually produces the individual albums, to keep a running count? I think we can agree that it isn't the job of the individual albums, but the job of the Album class to keep a count of all of the instances it produces."

A class variable is written like : @@albumcount 
seting this class variable to 0 , it can now be treated like any other variable.

```class Album
  @@album_count = 0 
 
  def initialize
    @@album_count += 1
  end
 
  def self.count
    @@album_count
  end
end```

