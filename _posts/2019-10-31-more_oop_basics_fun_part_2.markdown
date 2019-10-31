---
layout: post
title:      "More OOP Basics Fun! Part 2"
date:       2019-10-31 13:07:44 +0000
permalink:  more_oop_basics_fun_part_2
---


1. Class Constancts: as the name implies a class constant is a box whose contents are accessable to all methods within a class. In the case of our Books.rb labs it is defined like this:
```class Book
  attr_accessor :author, :page_count, :genre
  attr_reader :title
 
  GENRES = []
 
  def initialize(title)
    @title = title
  end
 
  def turn_page
    puts "Flipping the page...wow, you read fast!"
  end
 
end```

2. Since the Spec test for this project expects GENRES to store the genres into a list we have to decide where that is supposed to happen. 
Here is the test :
```describe 'GENRES' do
  it 'keeps track of all genres' do
    genres = ["Thriller", "Science Fiction", "Romance"]
    genres.each_with_index do |genre, i|
      book = Book.new("Book_#{i}")
      book.genre = genre
    end
 
    genres.each do |genre|
      expect(Book::GENRES).to include(genre)
    end
  end
end```

it shows us that :
The test is creating a bunch of books.
The test is assigning each of those books a genre.
The test is expecting our GENRES class constant to keep track of those genres.

so when should we store that genre into GENRES? In step 2!

3. it is important to point out that we need to make so essential changes to our program. First we need to remove the attr_ accessor for genre because we now do not need to write(set) AND get the information. We are instantly passing that data into the GENRES array. We change that to attr_reader so we can still read genre.

1. Explicitly define the genre= method, to integrate our class constant into the method
2. Remove the attr_accessor for :genre since we no longer need to generate a reader AND a writer.
3. Add an attr_reader for :genre, since we still want Ruby to generate a reader for us.

```# book.rb
 
class Book
  attr_accessor :author, :page_count  # remove the attr_accessor for genre
  attr_reader :title, :genre  # add an attr_reader for genre
 
  GENRES = []
 
  def initialize(title)
    @title = title
  end
 
  def turn_page
    puts "Flipping the page...wow, you read fast!"
  end
 
  # create the writer for genre and add the logic for the class constant
  def genre=(genre)
    @genre = genre
    GENRES << genre 
  end
end```

now we have a varible that will keep track of all the genres for every book created. 

