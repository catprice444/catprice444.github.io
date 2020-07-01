---
layout: post
title:      "CLI Project- My rollercoaster"
date:       2020-07-01 22:42:08 +0000
permalink:  cli_project-_my_rollercoaster
---


Going into the CLI Project I was scared. I did not have a lot of confidence in myself and the thought of having to do this on my own was honestly frightening. I wanted to make sure that I did a cool project and that actually had some value for myself. This is when I decided to do a project about rollercoasters and scraping the information from the amusement park's website so I can learn more about each ride that I choose. 

My project would start by welcoming the user to the park and then outputing the list of rides/ attractions in the park. It would then prompt the user to choose a ride, then spitting out the relevant information. The user would then be asked if they would like to see more rides, or exit out of of the system. If they chose to continue, it would start the process over again. If they chose to exit, the program would close out. 

After watching a couple of Learn.co videos about the CLI project, to gain some confidence, I decided I just needed to dive in and start coding. I was genuinely surprised by my abilities and how much I got done on the first day. I followed Avi's advice of using fake data to get the basics running and would work on scraping the information later.  I worked through the cli and got that working with the fake data and was happy with my success on that first Saturday (granted it took about 10 hours but nonetheless still happy). 

Then came the day I was supposed to scrape information. At first I had decided to try scraping the Cedar Park website, that was extremely frustrating because almost 4 hours later I was still getting minimual information from the site. I started to question my original code and wondered if I need to change it. (I found out later that week that the website was written in Javascript so my basic understanding of HTML scraping was not helping me scrape it.)
So after looking at several more websites for one written in HTML, I finally decided to use Kennywood's website. (Kennywood is a small amusement park located in Pittsburgh, PA, my hometown.)

Finally, I had a website and I was determined to finish it. After looking at the first couple of rides I decided I was going to scrape the ride's name, disclaimer, description, details page url, minimum height requirement, and thrill level. I then spent the next several hours attempting to figure out how to get the min height and thrill level scraped off of the details page. 

Most of the information was decently easy but their website is set up with similar class names, so I had to figure out how to get the information based off of what it was. I remembered I had done something similar in the scraping lab and reviewed that lesson and went to work. I finally came up with:

```
all = {}
     indiv_ride.css("div.default_button").each do |info|
     if info.css("span.title_attribute").text.include?("Minimum Height")
       all[:min_height] = info.css("span.title_value").text
		elsif info.css("span.title_attribute").text.include?("Thrill Level")
		  all[:thrill_level] = info.css("span.title_value").text
			
		end 
		all
end 
		
```

I was so happy to have finally cracked the code on how to get all the information I needed. I started to test my code and BAM it broke. I felt defeated and confused. What did I do wrong? After some investigation I realized that out of the 48 different attractions Kennywood had, only 9 of them had a seperate details page. This led to a lot of frustration that I had just completed all that coding for nothing, but I was hopeful I could still pull that information. Luckily all of those rides have a section for those attributes on the main page of the website. 

Since all of the information I now needed was on one page, I decided to make the code as simple as possible to hopefully get the best result. I continued with doing an 'each' statement to extract the data and set it so the pulled information for each set of coasters was pushed into the @@all array upon initialize. After a lot of frustration and a lot of googling "how to scrape", and attending an open office hours study group (where he was able to help me fix a very simple, and stupid problem that I had been overlooking) I FINALLY got the scrape to work:

```
def self.scrape
    website = Nokogiri::HTML(open("https://www.kennywood.com/attractions"))
    rides = website.css("div.pcore2_tile_copy")
    
    rides.each do |ride|
      indiv_ride = Kennywood::Coasters.new
      indiv_ride.name = ride.css("h2").text
      indiv_ride.disclaimer = ride.css("i").text
      indiv_ride.description = ride.css("p").text
      indiv_ride.url = ride.css("a").map { |link| link['href'] }
      indiv_ride.about = ride.css("div.pcore_tiles_attribicons").children.map {|att| att.text}
      end

    end
```

That moment of elation was amazing. But overall I was glad to be at the end of the rollercoaster, excited about the ride I had experienced.


