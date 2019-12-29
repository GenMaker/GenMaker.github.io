---
layout: post
title:      "FirstCDI Project"
date:       2019-12-29 05:37:16 +0000
permalink:  firstcdi_project
---


Horray!  I have learned alot and now I  am at my first portfolio project. Make a Command Line application that scrapes information from an active website.

**What's the big Idea:**
I see all the neat possibilites for an application. After overcoming the intilal paralysis, I landed on this idea:

**Animal Rolodex**
I want to create a learning app to discover and learn about animals that they may have never heard of before. I teach and often when I ask students to think of an animal they come up with the same list. Dog, cat, cow, pig, elephant...etc. There are so many cool and unusal animals in the world and even as an adult I am still amazed at the diversity of life on our little blue marble.  Using a suggested checklist from a learn co video:

1. Plan My Gem, Imagine your user interface
      I want to build my app based on the National Geographic Online Animal Encyclopedia website. This is a well organized page that has animals divided by catagory like mammal, birds, reptiles, even prehistoric.  The app will ask the user: 
			1. app will ask :what kind of animal do they want to learn about today. mammals, reptiles, etc
			2. The user will select a catagory, by typing a word option
			3. Then the app would present to them a choice of animal features like , number of legs, scales or no scales, oviperous or live birth, live span, habitat.  User enters a number for each option-  Maybe two  imputs
			4. Then the app will random generate a results that fit the selected criteria. 
			5. The app will list the site's fast facts about this animal and 
			6. a link to the page on national geographic to learn more.   
			
			What might change:
			I anticipate some changes from my idea will be what the cli will be able to ask the user for input. For instance, is there a good way for me to scrape how many legs an alligator has so that can be a criteria for the user to select?  
			I don't yet know for sure how I can generate an array of selected animals and then randomly present an animal so that the user doesn't get the same animal for a set of criteria all the time. I have a feeling there will be the % modulus and some complex math acting on the array. 
		
		After initial coach discussion:
		Scope: for this first iteration - simplify - may be only scrape the name of an animal, then the program will scrape one page of information and then it would present just the name of the animal.  With a feature of random selection.   
	
	Change: after the planning meeting with coach Beth we figured out that national geographic is not a good scrapable site. I am changing to https://a-z-animals.com/ 
	

2. Start with Project Structure - 
     Initital file set up means that I build some basic relationships with the different files. I know where my cli controller methods are , where I am holding all my require commands, and where the whole program is being called.  
		 Update: two weeks into the project I am struggling with organization. There are many  crossing interactions. I have worked out the rough mechanics of how all the pieces work it is like putting together a puzzle where I have to shave the edges a bit. ;-)
		 
		 
3. Start with Entry point - file run 
     We test the initial file set up to make sure that the file will load. In this case I did not have a consistant name for my class- typing in Animal_Rolodex when it should have been AnimalRolodex. I was able to print out a welcome message to the user. I am planing out the application by roughing out what methods I think I will need.  
```
	class CLI
  def run 
    Play.welcome
    make_animals
    play
  end

```

4. Scraper- 
     The site has an index page where it has organized all animals in an a-z order.   I think this will be a good place to create Animal objects from, this is the first scraper. 
```
 
		 class Scraper
   BASE_PATH = "https://a-z-animals.com/animals"
   
      def self.scrape_page                  #creates a hash of animal names 
        animal_name=[]
        doc = Nokogiri::HTML(open(BASE_PATH)) 
        doc.css("div li").each do |animal|
          animal_name << {name: animal.text, url: animal.css("a").attr("href").value}
        end
        animal_name.shift(12)
        animal_name
      end

``` 
	 
	The second scraper is set to scrape the data page of the induviual animal being featured.
		
	```def self.scrape_animal_text(animal) #scrapes selected animal page
			animal_url= "https://a-z-animals.com" + animal
			doc2 = Nokogiri::HTML(open(animal_url))
			    animal_noko_data = doc2.search("p")
          animal_noko_data
      end
end
			```
			
5. Make Animals- 
       I'll need to create Animal Objects to hold information. I can imagine that in the future this app can grow to become a personal encylopidia for the user.  The process of making objects for this project was the point of largest imporvement for me. Mainly, the benifit of using objects as opposed to hashes or arrays. In my first try this was my Animal.new method.
			 
		```def self.animal_data(data)       #creates hash of all data from selected animal
		info = []	     
		animal_data.each do |i|	      
		 info << i.text	        
		end	 ```     
     
		 It wasn't put together in my head until after a coaching session that a hash is not as deft as creating actual objects right at the start.  
		 
		 class Animal
  attr_accessor :name, :url, :text
  @@all = []
  
```
  def initialize(name, url = nil, text = nil)
      @name = name
      @url = url
      @text = text
      @@all << self    
  end
  
  def self.create_from_list(animal_array) #create animal objects name and url and text
    animal_array.each do |animal|
      new_animal = Animal.new(animal[:name], animal[:url], animal[:text])     
    end
   
  end
```

		 
5. Play-
     Play class is were all the fun is. This class holds methods for welcome and good bye. I especially enjoy the goodbye suggestions to the user after learning about their new animal.
		```
 def self.goodbye
    puts " _______________________________________________________________________"
    puts "  Thanks for checking out your animal rolodex. Additional project ideas:" 
    puts "  1. Draw a picture of your #{@star_animal.name}."
    puts "  2. Play pretend that you are a #{@star_animal.name}."
    puts "  3. Tell your Mom or Dad all about the #{@star_animal.name}."
    puts "  Goodbye! Till we spin again!"
    puts " _______________________________________________________________________"
  end
```

The  play method holds all the control for the interation after the initial cli run. 

```
def self.play 
    puts "\n"
    puts "            Enter '!' to spin your rolodex. Type 'exit' if you are done."
    @input = gets.strip
    counter = 0
    if counter <= 2
      if @input == "!"
        counter += 1
        @star_animal = Animal.select_animal
        learn_more
      elsif @input == "exit" || @input == "Exit"
        goodbye
      else @input != "!" || @input != "exit" || @input !="Exit"
        puts "Opps make sure you type in ! or exit"
        pla, 
      end
    end
  end
```


6. What are the biggest learning moments:
     I learned how to and why making objects are valuable. I still have a lot to learn about what methods are out there to make the application more sophisicatied.   I learned how to pass information around between classes. Finally, I struggled continually with organization of what methods should be where and what class responsibilites are. I think the final version , while there remains lots of room for improvement,  is organized resonably well. 

		 


