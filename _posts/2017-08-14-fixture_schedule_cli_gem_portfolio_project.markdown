---
layout: post
title:  "'Fixture Schedule' CLI Gem Portfolio Project"
date:   2017-08-14 21:44:04 +0000
---


## Where Do I Begin??
I have, just now, completed my very first portfolio project for the CLI Gem Data Assignment.

I chose to create a gem that would utilize the skills I have learned with OO Ruby, Scraping, Object Architecture, Instance Variables, and much more. All of these components helped to create the final product which is a soccer schedule gem that outputs the data collected from the Fox Sports website and lets the user interact with by giving choices for commands and various paths to take.

Starting the project proved to be as much of a challenge as was writing the code because I did not know what was considered either too difficult for my skill level or even that which may be considered too easy for all that I have learned so far. In the end, it took some interaction with students at an on-campus study session for me to gather the inspiration to work on something that I thought would be useful (at least based on what I would consider useful). As such, I created a fixtures schedule.

## The Low-Down of My Gem

The basic structure welcomes the user with a menu and an image of a soccer ball which I found on the internet and thought was pretty cool. 

```
  ▓▓▓▓▓▓▓▓▓▓▓▓████████████
        ▓▓▓▓▓▓▓▓███████▒▒▒▒▒▒▒▒▒███
        ▓▓▓▓▓█████████▒▒▒▒▒▒▒▒▒▒▒▒████
        ▓▓▓▓██▒███▒▒▒▒██▒▒▒▒▒▒▒▒▒█▒▒▒██
        ▓▓▓█▒▒▒█▒▒▒▒▒▒▒▒█▒▒▒▒▒▒▒█▒▒▒▒▒▒██
        ▓▓█▒▒▒█▒▒▒▒▒▒▒▒▒▒████████▒▒▒▒▒▒▒██
        ▓█▒▒▒██▒▒▒▒▒▒▒▒▒█████████▒▒▒▒▒▒▒▒█
        ██▒▒▒█▒▒▒▒▒▒▒▒▒▒██████████▒▒▒▒▒▒▒▒█
        █▒▒▒██▒▒▒▒▒▒▒▒████████████▒▒▒▒▒▒▒▒█
        █▒▒█████▒▒▒███▒▒▒███████▒▒████▒▒▒██
        ███████████▒▒▒▒▒▒▒▒███▒▒▒▒▒▒▒▒█████
        █▒███████▒▒▒▒▒▒▒▒▒▒▒█▒▒▒▒▒▒▒▒▒▒████
        █▒███████▒▒▒▒▒▒▒▒▒▒▒█▒▒▒▒▒▒▒▒▒▒████
        ▓█▒██████▒▒▒▒▒▒▒▒▒▒██▒▒▒▒▒▒▒▒▒▒███
        ▓▓█▒██▒▒██▒▒▒▒▒▒▒▒▒█▒▒▒▒▒▒▒▒▒██▒██
        ▓▓▓██▒▒▒▒▒███▒▒▒▒█████▒▒▒▒███▒▒▒█
        ▓▓▓▓██▒▒▒▒▒▒███████████████▒▒▒██
        ▓▓▓▓▓███▒▒▒▒▒▒██████████▒▒▒▒██
        ▓▓▓▓▓▓▓████▒▒▒█████████▒▒███
        ▓▓▓▓▓▓▓▓▓▓█████▒▒▒▒▒▒████ 
```

The gem then goes on to list the three best league names in the soccer world (English Premier League [EPL], Spanish La Liga, and Italian Serie A) which the user can then go on to discover the next upcoming games.

After viewing the list of fixtures, the user is then able to re-list the leagues and loop through the gem or they can choose to exit (or, as the program calls it, "blow the final whistle") and end the gem.

## What Can I Improve?

As of this moment I have not had the final review with an instructor so I do not believe the gem is at it's best and can be inmproved with some refactoring and additional interactivity through further objects; however, for it being my very first project, created from scratch, I am very pround of it.

Some aspects that I believe can be ammended include introducing the dates of the various games, formatting the list to a more readable structure, and including the entire list of fixtures for the season. 

The dates of the games is a vital component of a fixture schedule but I was unable to format the final result as I wanted it to appear for the user. I used a combination of scraping and Regular Expressions to comb the website for the information and format it without glaring whitespace, which proved to be extremely difficult. Below is my final product of the scraping line for the EPL scraper.

```
  la_liga = Nokogiri::HTML(open("http://www.foxsports.com/soccer/schedule?competition=2"))
    la_liga.css("table.wisbb_scheduleTable").collect do |fixture|
      fixture_info = {
        #binding.pry
        :all_info => fixture.css("tbody").text.gsub(/\s+/, " ").strip,
      }
```

I believe that with some refactoring I can fine tune the information to create the ability to scrape just the team names, dates, time, and locations from the website. This will be addressed at a later date and perhaps with some assisstance.

The format of the list also proved to be a great challenge for me on this project. In the end, I found the final product to be readable but I can see how it may need to be touched up in order for a new user to be able to interpret it correctly.

Finally, I was dissappointed that I was unable to include the entire fixture list of the season in my gem. I tried multiple combinations of the various HTML tags but the only one that worked for me (shown above) still did not provide my desired end product. Again, I believe this can be fixed but I will look for some help in order to do so.

## In Conclusion
To wrap this up, I am extremley proud of the gem that I created. I think that the interactivity is easy to comprehend for the user, the load time is extremely fast, and the overall structure is easy to expand upon which will be useful in the future. I also worked to keep my code as abstract as possible and I think I accomplished that objective. My objects are self explanatory and I stuck to the single-responsibility principle. These best practices are very important when writing code and it is a great pleasure that I was able to implement them on my very first project. 

I look forward to the instructor session where I can learn even more from my mistakes and improve this gem to make it as best as it can possibly be.

Until next time,
AA
