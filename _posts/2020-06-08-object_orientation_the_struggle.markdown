---
layout: post
title:      "Object Orientation, the struggle"
date:       2020-06-08 11:28:30 +0000
permalink:  object_orientation_the_struggle
---


Do you ever have those moments when you are confident and just feeling like the "wiz kid" learning a new lesson. You think "this is easy" or "I got this". Then all of a sudden, the rug gets pulled out from underneath you. Object Orientation did that to me. 

Started off strong learning about class methods and their relationships to instances. Breezed through the labs involving making a dog bark and involving self in the code, then the has-many-objects lessons hit. This is where I started to struggle. 

Has-many-objects, in the simplistic of terms, means connecting class methods so they talk to each other. An example in many of the labs was the connection between an artist, their song, and the genre of the song. Obviously all these things are connected, but its how they are connected that really messed me up at first. If you think about it. A song cannot exist with an artist or a genre. And a artist cannot exist without a genre. But a genre can exist without the song or artist. So now how do you put all those items together. 

To be able to connect the class methods, one of the first things you have to do is put an `attr_accessor` into the class of the child methods. You can see an example of this in the song method:

```
class Song
   attr_accessor :genre, :artist, :name
	 @@all = [ ]
end 
```

Since the song cannot exist without the genre or the artist, we would need to include both of those class methods in the `attr_accessor` code. By including the genre and artist you are able to connect the code of the song class with the parent methods. 

By connecting these methods you are able to iterate over the code from a different class in the class you're working in. For example if I am trying to find all of the songs that belong to an artist. I am able to write:

```
class Artist
def songs 
    Song.all.select {|song| song.artist == self}
  end
end 
```

Notice how we used the class method of song to iterate over all of the songs and find the one whose artist of the song is equal to self. 

While I am definitely feeling like I am getting a better sense of how to connect my class methods, I am still very much in the learning stages. I keep having to remind myself that this is all part of the process of coding and it's okay to be confused. Thats when you know you're truly working hard. 
