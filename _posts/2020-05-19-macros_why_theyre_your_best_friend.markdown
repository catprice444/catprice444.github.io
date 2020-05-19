---
layout: post
title:      "Macros: why they're your best friend"
date:       2020-05-19 11:45:39 +0000
permalink:  macros_why_theyre_your_best_friend
---

One of the best parts about writting in Ruby, is all the ways we can de-clutter our code. Macros are one of those ways. 

When writting a class, you want to be able to both call upon it, and also write within it. Respectfully these actions within our code are called readers and writers. To write both a reader and a writer for a single instance variable, it would take at least 6 lines of code to accomplish. 

To write out a class for a camera with an instance variable "lens" your code would look something like this:

```
class Camera

    def lens=(lens)
		    @lens = lens
		end
		
		def lens
		   @lens
			 end 
			 
end
```

That is a lot of lines and repetative coding to accomplish such a small task, imagine if you also wanted to be able to include the type of camera, year it was made, the condition it is in, who the owner is, etc. The options for ways you could describe items that make up a camera are endless. All of those items though make up 6 more lines of code, soon your code starts to become long and crowded. This makes it hard to fix errors in the future and also troubleshoot the code before you finish. 

But fear not- Ruby has given us a fun and easy tool for combating all those lines of code. We call them macros. Macros are prebuilt code that help us write a repetative code in one line. One of the most common examples of macros are called attributes. There are three types of attributes: an attribute accessor, an attribute reader, and an attribute writer. 

The attribute accessor (or #attr_accessor) is the most common and it encompasses both the reader and writer lines  of code. I could write the camera lens instance variable using just the #attr_accessor macro in one line. 

```
class Camera

    attr_accessor :lens
		
end 
```

The attribute reader (or #attr_reader) is another common macro and it helps us create a getter method or a way for us to pull that line of code to read what type of lens we have assigned that camera. The #attr_reader would replace only 3 lines of code. This method is useful for when you want to be able to be able to read the code without writing on it or changing it after it has been assigned. 

```
class Camera

   attr_reader :lens
	 
end 
```

> replaces this line of code:
>  def lens=(lens)
> 	    @lens = lens
> 	 end 


The final type, and least common is the attribute writer (or #attr_writer). It is very uncommon to have an #attr_writer in your code without an #attr_reader. By just having an #attr_writer it would allow me to constantly change, or write on, the type of lens I have on my camera, but it wouldn't allow me to read it. 

```
class Camera

   attr_writer :lens 

end 
```

> 	 replaces this line of code:
> 	 def lens
> 	    @lens
> 	 end

By using macros, it helps to simply our code and makes our lives easier in the process. Both when writing the code and when fixing errors that might pop up in the future. 
