---
layout: post
title:      "How I gained a new respect for Javascript"
date:       2021-04-18 18:46:36 +0000
permalink:  how_i_gained_a_new_respect_for_javascript
---


Coming up on my Javascript project, I was nervous to say the least. I felt like this section made the least amount of sense and I was struggling the entire time. I feared for my abilities and how long it would take me to complete this project. After spending several hours trying to figure out an idea for my project - I landed on a meal planner. I have been wanting a place to keep all my recipes digitally, so why not try to make one for myself. 

After struggling to get the project started, I realized very quickly how confused I was. I occured to me in that moment that this section didn't have any video's. I love watching the coding video's, and a lot of time it helps to clear up confusion. I quickly decided it would be in my best interest to watch a bunch of Javascript videos first, and then start on the project. I spent the next day and a half watching video after video, and taking countless notes, on the Learn.co video lectures website. I came out feeling confident, and definitely less confused. 

While the project was certainly not easy, the more I worked with Javascript, the more I started to like it. Its pretty cool that AJAX functions exist. Its pretty cool that they work together with Rails and CSS to create an entire webpage without refreshing it, but you can still submit items and manipulate the page. 

One of the first struggles I came across revolved around a button. I wanted to be able to toggle my form on and off, this meant I would need a button with an event listener, allowing the page to show the form. But in my boldness, I also wanted to be able to close the form and hide it on the page once you were done with it. This caused a lot of issues. I couldn't figure out why the button was only working once. If I clicked it, it would toggle the form to "visible", but then wouldn't work again until I refreshed the page. Obviously that was no good. 

I worked on that answer for hours, researching everything I could think of, sitting in on a study group, but nothing seemed to work. Once I finally figured it out, it became obvious. It was one of those problems like "Why didn't I think about that before". I could use an if statement and the CSS styling to show or hide the form. 

```
 button.addEventListener("click", () => {
        if (form.style.visibility === "hidden"){
            form.style.visibility = "visible";
            button.innerText = "Close Form";
        } else { 
            form.style.visibility = "hidden";
            button.innerText = "Add a New Meal!";
        } 
    });
```

It was a great moment to say the least, and I went on to use that method in several other places in my code. I probably put too many buttons on the page, but I was having too much fun toggling items on/ off. 

Through this I also learned a lot about CSS styling, how you can "float" an object on the page, or adjust the size based on how large the object is. It was also fun to add styling to a parent element, but then add styling to different child elements. I also spent way too much time playing with these features. 

Overall, I am really proud of myself for how much I learned through this project. I am glad I took the time to watch videos and I am glad I kept a positive attitude throughout. I can't believe I only have one more project left and how far I have come over the past year. 
