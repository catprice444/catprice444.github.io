---
layout: post
title:      "Sinatra Project- Timesheet app"
date:       2021-01-11 06:08:26 +0000
permalink:  sinatra_project-_timesheet_app
---


For my sinatra project I decided to make an application that would allow users to enter in the days they worked, to help track for timesheets. 

The basic premise of my application is fairly simple. Each person is able to create a unique account that allows them to create, read, edit and delete different days they worked. Every person who creates an account is able to see the entire listing of all the days worked, however, only the user who actually created those workdays is able to edit and delete them. 

I did this through the CRUD model we have been learning throughout the sinatra lessons. The application has a workday model and user model. The user model has many workdays while the workdays belong to a user. I then created an application controller, user controller and workday controller, while also creating the appropriate views for each page of my application. 

The work within my controllers models is what I am most proud of. I started off by following the steps I have learned in the past labs like creating helpers methods within my application controller,

```
helpers do 
    def current_user 
      User.find(session[:user_id])
    end 

    def logged_in?
      !!session[:user_id]
    end

```

and the basic CRUD model methods of creating an index, new, show, edit and delete actions. It was when I started to customize my application that I felt I learned the most. I learned how to create error messages on a page through different validations. 

An example of this is when a user attempts to login but is entering an invalid username/ password. The screen pops up with a message at the top, telling the user it is invalid. 

```
   post "/login" do 
        @user = User.find_by(:username => params[:username])
        if @user && @user.authenticate(params[:password])
            session[:user_id] = @user.id
            redirect to "/workdays"
        else 
            flash[:error] = "Invalid username/ password. Please enter correct information or visit sign-up page"
            redirect to "/login"
        end 
    end 
```

You can see through my post method, on the login method of the user controller, that there is a flash error message that will appear anytime a person attempts to login and the system cannot find a username and password to match. 

On the login view page you can see where the message would be displayed on the page. The error message does not appear at first, it only shows up in that location once it has been triggered by the post method above. You can see on this page there are two other messages that could appear. While those are triggered through seperate methods in the user controller, they are still only visible after a user has completed a certain action. In the case of these messages, it would give the user notification if they logged out successfully, or if they attempted to view the timesheets app without being logged in. 

```
<h1>Login</h1>
<br>
</br>

<p class="login-message"><%= flash[:login] %></p>
<p class="logout-message"><%= flash[:logout] %></p>
<p class="error-message"><%= flash[:error] %></p>

<form action="/login" method="post">
    <h3>Username:<input type="text" name="username"></h3>
    <h3>Password:<input type="text" name="password"></h3>
    <input type="submit" value="Login">
</form>

<br>
</br>

<h3><a href="/signup">OR SIGNUP HERE</a></h3>

```

I got really excited when I found how to validate the information being put into a workday with appropriate error messages. 

I wanted to make sure that when a user entered a workday, they would not be able to enter a day with the shift ending date before the shift start date. This validation would need to be in both the creation of a new workday, and also any editing afterwards. 

```
   post '/workdays' do 
        if current_user.nil?
            flash[:error] = "Please login or sign up"
            redirect '/login'

        elsif params[:shift_start] == "" || params[:shift_start_time] == "" || params[:shift_end] == "" || params[:shift_end_time] == ""
            flash[:error] = "Fill in all fields to submit form"
            redirect '/workdays/new'

        elsif (params[:shift_start] > params[:shift_end])
            flash[:error] = "Check dates"
            redirect '/workdays/new'

        else 
            @workday = Workday.new(:shift_start => params[:shift_start], :shift_end => params[:shift_end], 
                :shift_start_time => params[:shift_start_time], :shift_end_time => params[:shift_end_time], 
                :notes => params[:notes])
            @workday.user_id = current_user.id
            @workday.save
            redirect "/workdays/#{@workday.id}"
        end 
        redirect '/workdays'
    end 
```

My create action with the post method was the most complex as it had to have several validations to make sure the user was entering good data. It starts with making sure that there is a current user logged in, if not it will direct them back to the login page, and flash the error message we saw on the login view page. Next, the system will check to make sure that all fields have been filled out before they can submit. If it is false, it will throw the error message you see above and have the user fix those issues. Then it will confirm that the start date is greater than end date. If that becomes false it will throw another error. 

Once all of those tests come back as true, only then will it create the new workday. When creating the new workday it also saves the workday user id as the current user id, this helps to make sure that later on another user does not edit or delete this particular workday. 

Overall I had a lot of fun building up this application. It was stressful at times from the randoms errors it would throw. But thanks to the slack community, I was able to persevere and finish my second project.







