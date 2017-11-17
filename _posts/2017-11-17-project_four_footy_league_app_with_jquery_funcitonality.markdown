---
layout: post
title:      "Project Four: Footy League App with jQuery Funcitonality"
date:       2017-11-17 14:59:23 +0000
permalink:  project_four_footy_league_app_with_jquery_funcitonality
---


For the fourth assessment project of my [Flatiron Curriculum](https://learn.co/alecgalba), I was required to build a jQuery front end to my previous project. You can read about the making of the Footy League App on [this blog post](http://alecalba.com/ruby_on_rails_portfolio_project) and check out the complete code files via my [Github](https://github.com/alecgalba/footy-league-rails-app). Despite the original build of the app taking a longer duration of time, the fact that this was also the first project in which I used my newfound JavaScript knowledge made it a much more difficult project.  However, I believe that I learned a lot from the frustration of hijacking some links and rendering dynamically responsive layouts.


### Project Requirements Layout:
1.	Must render one index page via jQuery and an Active Model Serialization JSON Backend.
I had multiple models to choose from (Teams, Leagues, Users, Fixtures, and Comments), but since my last project focused on adding functionality to the Team models, I decided that I would improve the user experience of the League models with this capability.
•	The League Index page has a “More Info” link that expands the description section for each League to allow users to read about the specifics of the league and decide if they want more information before navigating to the specific show page.

2. Must render one show page via jQuery and an Active Model Serialization JSON Backend.
For this requirement, I decided to improve the functionality of the Fixture models.
•	Fixtures show page has a “Next” button that allows the user to navigate through all the fixtures without redirecting the user through the index page.

3. The Rails API must reveal at least one has-many relationship in the JSON that is then rendered to the page.
•	In the League show page, a User has many Comments.

4. Must use your Rails API to create a resource and render the response without a page refresh.
This meant that for example, if a user adds a comment to a post, the comment would be serialized, submitted via an AJAX POST request, with the response being the new object in JSON and then appending that new comment to the DOM. In other words, I was supposed to use an AJAX post to create a new object. I chose to create a new comment.
•	Within the League show page, you can create a new comment and the new comment will appear on the same page by exposing the new data in a hidden div, with no refresh.

5. Must translate the JSON responses into Javascript Model Objects. The Model Objects must have at least one method on the prototype. Formatters work really well for this.
This requirement meant that the JSON responses must be turned into JavaScript objects first before the updated data was rendered to the page. So for example I click on a specific League (in JSON), and then take the info I needed to create a JavaScript Comment object. Then I’d take that object and use it in the rendering of the information. Also, I’d have to add a method to the prototype.
•	Comment has a formatComment() function.

### Active Model Serializer Gem:
One of the first things I did was install the Active Model Serializers (AMS) gem. This allowed me to create the JSON, so I could use it in my Leagues and Fixtures index and show views.
The AMS gem is a convention based approach to providing serialized resources in a “Rails-y” way. What this means is that I was able to bypass the time-consuming work of building JSON objects by hand using pre-formatted strings. Similarly, I was able to implicity call the serializer from my controller rather than explicitly calling it if I would have used the “to_json” convention. With all of this information, I could use it to render the specific information needed for my index and show pages.

The next thing that I did was to add some front-end functionality to the League index page. The first version had a table of the built Leagues, with the entire description available to the user. I thought it would add to the user experience if they were able to hide the information that they didn’t want under “More Info” buttons so as to de-clutter the table and bring uniformity to the display. The User could then click to read the rest of a description to see if they wanted Team and Fixture data about the specific League or click a different League’s info button. Below is the code that adds this funcitonality:
```
<td id="league-<%= league.id %>"><%= truncate(league.description) %><button class="js-more" data-id="<%= league.id %>">More Info</button></td>
.
.
.
$(function() {
  $(".js-more").on("click", function() {
    var id = $(this).data("id");
    $.get("/leagues/" + id + ".json", function(league) {
      var descriptionText = "<p>" + league["description"] + "</p>"
      $("#league-" + id).html(descriptionText);
    });
  });
});
```


This code uses the truncate helper method. When a user clicks the “More Info” link, they see the full description text.

### Creating the Comment Object Using JavaScript Model Objects:
One aspect that makes comments such a vital feature on the Internet is the identification of the user contributing to the application. When I was working on using my Rails API and a form to create a comment and render the response without a page refresh, each of my comments were missing an identification in the console. So that had to be fixed. In order to resolve that issue I had to create a customized comment_list serializer under the League Serializer (since Comments belonged to Leagues) in order for each comment to have their own user identification via their email, as shown below:

```
class LeagueSerializer < ActiveModel::Serializer
  attributes :id, :name, :description
  has_one :user


  def comment_list
    object.comments.map do |comment|
      {
        id: comment.id,
        user: {
          id: comment.user_id,
          email: User.find(comment.user_id).email
        },
        content: comment.content
      }
    end
  end
end
```

Via Object Orient JavaScript I created a constructor function to build a prototype for what an object (comment) would look like, including all the properties (id, content, and user). Additonally, I added a formatComment() method to this object as well to properly format the comment output. Below is the code:

```
$(function() {
  function Comment(data) {
    this.id = data.id;
    this.content = data.content;
    this.user = data.user;
  }

  Comment.prototype.formatComment = function() {
    var html = "" ;
    html += "<div id=\'comment-\' + comment.id + '\'>" +  "<strong>" + this.user.email + "</strong>" + " says: " + this.content + "</div>";
    $("#submitted-comments").append(html);
  }

  $(function() {
    $(document).on("submit", "form#new_comment", function(event) {
      event.preventDefault();
      var $form = $(this);
      var action = $form.attr("action");
      // in order to process the comment(form data), its need to be converted from an object to a string.
      var params = $form.serialize();
      $.ajax({
        url: action,
        data: params,
        dataType: "json",
        method: "POST"
      })
      .success(function(json) {
        $(".commentBox").val("");
        var comment = new Comment(json);
        comment.formatComment();

      })
    })
  })

})
```

I learned many nuances of the jQuery and JSON world while working on this project, though I am aware that there is still much to learn. There are still some features I want to include, such as including the option for users to edit and delete comments as well as dynamically adding teams and players, but that will have to wait for V3. I look forward to learning React/Redux and continuing my journey of becoming a full stack web developer.

Onwards!

