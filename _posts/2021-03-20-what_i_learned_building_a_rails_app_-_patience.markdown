---
layout: post
title:      "What I learned building a Rails App - PATIENCE"
date:       2021-03-20 23:04:21 +0000
permalink:  what_i_learned_building_a_rails_app_-_patience
---

I decided to build an app based on the idea of the DonorsChoose website. For anyone who isn't familiar, its a website where teachers can submit items they need for their classroom then donors can donate money to help purchase those items. 

My model has 3 objects, User- School- Items. Building out these objects and developing the basic CRUD functionalities was the easy part. My issues started once I get cocky and wanted to add all these new things to the mix. My first issue came with the donation button. Obviously, for a donor to donate an item, you need a donation button. 

My main problem came with updating the appropriate fields once that donation button was submitted. I wanted to be able to erase the amount needed while also updating the user's donation amount ( a field the donor fills out saying how much money they want to give, ex: $500) to represent the recent donation. I was running into issues left and right, I would fix the code and then something else would break. I couldn't get the code to update the donation amount and erase the amount needed. I was getting so frustrating, googling everything I could thing of. Then it dawned on me, switch my code around. The system will run the code in order of what it hits first. So if I change the user donation amount first THEN tell it to erase the amount needed it should work. And bingo, it did. 

I ran into some other issues, but they all seemed minor to my biggest pain- OmniAuth. I hit every problem in the book with installing this thing. First it wouldn't recognize the provider, then it would post properly to google, then it would claim it was logging in but redirect back to the login screen and wouldn't actually login. Then after looking through my code for what I thought was the thousands time, I saw it! I had copied the omniauth code from a tutorial, and their session id code was just the slightest different than what I was using. 

The copied code `session[:user_id] = @user.id`
vs.
my code `session[:id] = @user.id`

See the difference? 

The tutorial code was putting the user id as the params for the sessions, rather than giving it its own id and making that also the user id. Finally, after finding that, and making the appropriate changes, I had my working omniauth code-

```
def google
        @user = User.find_or_create_by(email: auth["info"]["email"]) do |user|
            user.name = auth["info"]["first_name"]
            user.password = SecureRandom.hex(10)
        end
        if @user.valid?
            @user.save
            session[:id] = @user.id
            redirect_to user_path(@user)
        else
            redirect_to root_path
        end
    end 
    
    private 
    def auth
        request.env['omniauth.auth']
    end
```


Struggle after struggle over what now seems like the most minor of things when building this app. The thing I will take away from this lesson is definitely patience. Its probably the stupiest of reasons why its not working, so just take a deep breath, have a beer and look closely. You will find it, you just need some patience.



