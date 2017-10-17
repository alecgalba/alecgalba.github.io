---
layout: post
title:      "Ruby on Rails Portfolio Project"
date:       2017-10-17 16:21:55 +0000
permalink:  ruby_on_rails_portfolio_project
---


### What is my App?
For my third portfolio project I decided to improve upon my last project, the [Sinatra Soccer League application](http://alecalba.com/2017/09/18/sinatra_applications_the_best_is_yet_to_come/), because I knew there were more features that I could have added and I believe there was more for me to learn.

I built this application with the goal in mid of recreating a functional soccer league database where users could create teams, join leagues, set up fixtures, and populate their teams with player profiles. Not only does this subject matter interest me greatly, but also I found that the relationships between these features were a perfect fit for practicing database associations and resource manipulation that we have been practicing in the Ruby on Rails portion of the curriculum. A perfect hat-trick!

![](https://media.giphy.com/media/7DmfHPcyrm9eU/giphy.gif)

### What was my process?
As a side-note this was my first project after I graduated from using the Learn IDE as my main text editor and have now fully switched to my local environment using the Atom text editor. After [setting this environment up](http://help.learn.co/workflow-tips/local-environment/mac-osx-manual-environment-set-up-for-immersive-students), which was not simple for me, I was ready to begin the process.

I started my application as most people do for a new rails application: with the “rails new” command in my terminal. My next step was to include a user sign up and authentication system using the Devise and OmniAuth gems we learned about in the curriculum. It took some time, but after googling I found [this great resource](https://www.digitalocean.com/community/tutorials/how-to-configure-devise-and-omniauth-for-your-rails-application) for configuring your application with both gems from the start.

My next step was to configure my database with the rails generator helpers to set up associations and validations within the user, team, and league models. My models utilized `belongs_to`, `has_many`, `has_many, through`, and `has_and_belongs_to_many` relationships in order to establish full functionality between the models. Teams belonged to users as users could have many teams. Leagues and Teams both belonged to and had many of each other so that teams could persist through multiple leagues simultaneously. Interestingly enough, this was an issue that I highlighted in my previous project that I was now able to over come; so yay Rails!

###### Final User Model with Associations & Validations
```
class User < ApplicationRecord
  has_many :teams
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :trackable, :validatable,
         :omniauthable, :omniauth_providers => [:facebook]

  def self.from_omniauth(auth)
     where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
       user.provider = auth.provider
       user.uid = auth.uid
       user.email = auth.info.email
       user.password = Devise.friendly_token[0,20]
     end
  end
end
```

###### Final Team Model with Associations & Validations
```
class Team < ApplicationRecord
  belongs_to :user
  has_many :players
  has_many :fixtures
  has_many :leagues, through: :fixtures
  has_and_belongs_to_many :leagues

  validates :name, presence: true
  validates :mascot, presence: true
  validates :colors, presence: true

end
```

###### Final Leagues Model with Associations & Validations
```
class League < ApplicationRecord
  has_many :fixtures
  has_many :teams, through: :fixtures
  has_and_belongs_to_many :teams

  validates :name, presence: true
  validates :description, presence: true, length: {maximum: 50}

end
```

After testing and confirming functionality of the existing models, I created a nested resource of players to the teams so that a user could interact with a nested form to write to the parent resource, team. This process allowed for the RESTful URL of “teams/team:id/players/player:id” to exist and function.

###### Nested Resource Players under Teams
```
Rails.application.routes.draw do
.
.
.
  resources :teams do
    resources :players
  end
.
.
.
end
```

I then moved on to creating the “has many through” relationship between teams and leagues through fixtures. Each fixture is associated with a league and team by the team_id and the league_id. The fixture table acts as a join table and allows for user submittable attributes of date and time.

###### Fixtures Model with Associations and Validations
```
class Fixture < ApplicationRecord
  belongs_to :team
  belongs_to :league

  validates :opponent, presence: true
  validates :date, presence: true
  validates :time, presence: true

  scope :time, -> (time) { where time: time }
  scope :date, -> (date) { where date: date }

end
```

###### Fixtures Schema
```
  create_table "fixtures", force: :cascade do |t|
    t.string "opponent"
    t.date "date"
    t.time "time"
    t.integer "team_id"
    t.integer "league_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["league_id"], name: "index_fixtures_on_league_id"
    t.index ["team_id"], name: "index_fixtures_on_team_id"
  end
```

Players and Fixtures can be created through nested forms within teams and leagues which then allows for a series of fields such as team[player][0][age] or league[fixture][3][date]. As per the requirements I did not set this relationship up via the accepts nested attributes validation but instead through join tables for players and fixtures. I believe that this allowed more flexibility for querying the data in the rails console and could likely contribute to additional functionality for the application.

Finally I created class level scope methods for Fixtures and Players so that I could query the database for Fixture dates and times as well as Player ages and positions. These methods were written directly to the models, respectively, and could probably be enhanced even further.

### What was most challenging?
By far the most challenging aspect of this project was creating the “has many through” association between fixtures, teams, and leagues. After searching through the curriculum at the past lessons, parsing StackOverflow with great detail, and examining every bit of the Rails documentations I finally figured out the formula for creating this complicated association in my application. 

In the end I decided to model my fixtures join table after the comments join table that we have seen so many times with the Blog examples in the curriculum. While setting up the database and scaffolding the models were not an issue, I found that setting the attributes so that they aligned with the appropriate cross-referencing id’s for teams and leagues was the most challenging part. I found a work around that correctly associates the fixtures to a team and a league but I do need to work on the display of data.

Additionally, I struggled with setting up Devise and OmniAuth simultaneously but after following the link I provided above I was able to set it up rather quickly. I cannot recommend that link enough for someone who is struggling with this concept.

### What did I learn?
This portfolio project was many things for me. 

First, it was a new journey with an unfamiliar web framework, Rails, that I feel was extremely beneficial for my learning process. Reinforcing my knowledge of RESTful URLs, associations, database manipulation, and user display for an application will be vital for my career. I now feel like I have a working knowledge of these nuances that were kindled with my Sinatra project.

Second, this project was fulfilling in that I accomplished my goals set in my [Sinatra project blog](http://alecalba.com/2017/09/18/sinatra_applications_the_best_is_yet_to_come/) entry of including leagues, persisting teams through multiple leagues and gaining the ability to create player profiles. I am very proud of that.

Finally, this project was extremely challenging and was the first project that I decided to work from scratch rather that looking back at past labs or other student examples to further my progress. I gained great experience in searching the web for advice, using slack as an outlet, and attending study sessions when I needed.

### What can I improve?
Without a doubt the aspect that I want to improve on the most is creating a functioning `has_many, through` association that displays the proper information the way I had in mind. One lasting issue that I had with the project was the display of the fixtures within the index, show, and team show pages. Upon submitting this project, that is the primary issue that I would like to work on in the future.

### Conclusion
This Rails project allowed me to improve upon my Sinatra portfolio project in order to create a fully functioning soccer league database. The next evolution of this application will have, primarily, properly displayed associated data through the join table. An additional function could perhaps include an articles section that allows for users to post related articles or news blurbs about the application. Perhaps I could include admin privileges that moderate the creation of leagues and creates the fixtures. 

These things will come with time.

Onwards!

