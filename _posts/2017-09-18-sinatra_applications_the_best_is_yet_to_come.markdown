---
layout: post
title:  "Sinatra Applications: The Best Is Yet To Come"
date:   2017-09-18 19:48:12 +0000
---


### Sinatra Assessment Blog Post

This blog post will be detailing my efforts to create an MVC Sinatra application that mimics a soccer league database. The point of this project was to use [ActiveRecord](http://guides.rubyonrails.org/active_record_basics.html) and [Sinatra](http://www.sinatrarb.com/intro.html) with multiple interacting models to create this database and persist user data. My goal was to enable session cookies to persist this data as we have been practicing in the curriculum. Overall I am happy with the project although of course I see room for improvement.

### Models
My models included a user, and a team model. The user model was where the application's user could pass in their username, email, and password data that was then persisted to my database. This model worked just as expected and there were no issues once it was created.

The team and user models were linked through foreign keys "user_id" in my database so that a user could have many teams. I utilized a “has many” relationship between the models in order to allow this connection and it worked without any issues.
###### User Model
```
class User < ActiveRecord::Base
  has_many :teams
  has_secure_password
end
```
###### Team Model
```
class Team <ActiveRecord::Base
  belongs_to :user
end
```

### Views
The views presented a different challenge where I could be more creative and use the methods that I had built to present the user with an appropriate amount of options to personalize user experience.

The layout view was intrinsically linked with all of the other views by the yield method that is available in Sinatra. This layout view gets rendered everytime a new template is called within the same application ([Read More on Yield](http://www.sinatrarb.com/intro.html)). After getting the program working to my desire I was able to edit the various components of the application. I hope to fine-tune my CSS skills with other projects in the future but I am happy with the outcome presented here.

The user views included a user profile creation page, a user login page, and a user show page. These views presented little problems when constructing and I was happy with the outcome. I chose not to include any restrictions on email and password formats, however I did play around with RegEx a bit to see if I could include it in the final product. In the end it made the code much messier than I was hoping for so I eliminated it. Perhaps that is one area that I can include for the next project.

The teams views allowed for the full range of a CRUD application with create, update, read (show), and delete functions available for the user. The creation and reading components were simple to build but as mentioned above I had much difficulty with the updating and deleting portions of the application. After a pairing session with my learn instructor I was introduced to the [“build”](https://stackoverflow.com/questions/783584/ruby-on-rails-how-do-i-use-the-active-record-build-method-in-a-belongs-to-rel) method available in the ActiveRecord library which assigned a user id to the new instance of a team being created by the user. This method plugged a hole in my logic that then made it easier to build protection against other users manipulating the data created by the current user.
###### The Edit Route Final Code
```
  post "/teams" do
    if params["team"]["name"] == "" || params["team"]["mascot"] == "" || params["team"]["colors"] == ""
      erb :"teams/new"
    else
      @team = current_user.teams.build(:name => params["team"]["name"], :mascot => params["team"]["mascot"], :colors => params["team"]["colors"])
      @team.save
      redirect "/teams/#{@team.id}"
    end
  end
```

### Controllers
The most difficult controller to build was the teams controller because this contained the most functionality. The teams controller was responsible for creating new teams, showing the created teams, editing the created teams and deleting the created teams. Classic CRUD.

The editing and deleting routes were most difficult for me. For some reason I kept receiving an ActiveRecord error that indicated there was no “id” method for the team elements. This confused me because I was using the “id” method in multiple other routes within this application.

Little did I know that the solution to the edit route was as simple as adding the method “teams.id” into the show page itself (See code snippet below).
```
<% @teams.id %>
<h2>Team Name: </h2> <p><%= @teams.name %></p>
<h2>Team Mascot: </h2> <p><%= @teams.mascot %></p>
<h2>Team Colors: </h2> <p><%= @teams.colors %></p>
```
I was under the impression that the id value was being read from my teams controller page but in fact Sinatra was looking for the id method directly in the show page. Or at least that is how I solved it. Please correct me if that's wrong.

The solution to the delete route was also much simpler after I took a step back and reorganized the order of my teams controller code. After doing so it was clear to me that I needed to specify the delete route directly in the hidden portion of the from; something that I knew but that became muddled in the details when building the final product. Always connect those values!
```
<form method= "POST" action= "/teams/<%=@team.id%>/delete">
  <input type= "hidden" id= "hidden" name= "_method" value= "DELETE">
  <input type= "submit" value= "Delete Team">
</form>
```

### Satisfactions
In conclusion, this project gave me a week’s worth of headaches as I amassed over 60 hours in building, manipulating, breaking, and changing the code to build my first MVC Sinatra application. I am happy with my progress in the initial stages of building the layout and functionality between the user and team objects. I believe that I improved upon my method construction and “code-smell” that plagued me on my first project, the [Fixtures List Data Gem](http://alecalba.com/2017/08/14/fixture_schedule_cli_gem_portfolio_project/). Additionally, I believe that I used the extent of my knowledge from what I have learned so far in the Flatiron School program in this application and added a new arsenal of development language to my growing fundamentals. 

### Future Improvements
One important future improvement I will implement in v.2 is the inclusion of league and associating certain teams to multiple leagues as I tried in my initial build.  When it was present, I allowed for the existing teams to be presented in a checkbox format when creating a new league. While the leagues could be created without breaking the application, if a team was previously in a league and was checked into new league it would be deleted from the previous league in order to be presented in the new league. This was a slight bug that needs to be worked on otherwise teams would have to be created multiple times. As of now, only one league can exist under this format but I foresee an application that allows for multiple leagues to feature thousands of teams with each of these teams able to persist in multiple leagues simultaneously therefore simulating a real life recreational league database.

![](http://cache.lovethispic.com/uploaded_images/176108-Onward-To-Glory.jpg)
## Onwards!

