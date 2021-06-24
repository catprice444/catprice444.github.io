---
layout: post
title:      "Finally, I made it"
date:       2021-06-24 06:44:14 +0000
permalink:  finally_i_made_it
---


The last year has not been easy, to state the obvious. I've wanted to learn how to code for many years and when the world shut down last March, it seemed like the perfect time to learn a new skill. Learning a new skill while also dealing with the mental exhaustion of a pandemic was a lot harder than I ever thought. But I am proud to say that I have finally made it to this point. 

Out of all the lessons, React/Redux was by far the hardest. I spent the most time on this project, the majority of it just googling answers and watching videos explaining certain aspects. Like what is the difference between a functional component and a class component? For anyone else wondering - the simple answer is that a functional component is used to help display things and does not have a state. A class component does have a state.

For my project I decided to do a cocktail book. This book allows people to organize their cocktails by the main type of alcohol in them. They are able to add new types of alcohol and include a website that gives more information about it. They can also add and delete a cocktail associated with it. The cocktail includes a personal rating, recipe and ingredients needed. 

The part about this project I think I found so confusing and difficult was attempting to keep my component small. I kept feeling as if I was loosing my place in the project. I couldn't remember what items were in what components and if I needed to add anything to complete it. 

I also found it difficult attempting to figure out all the niche pieces of react or redux that make this app so flexible. An example of this was when I decided to add another reducer to my store. I wanted to pull state for my alcohols and cocktails. I currently had the alcohol state in my redux store, but I couldn't get the cocktails to mount. It confused the hell out of me because everything looked right. I had a componentDidMount in my container, I had a mapToStateProps and I was successfully fetching the data. But why wasn't it mounting. After an hour of research I found a small tidbit in an article that blew open the case. I needed to combine my reducers! 

```
import {combineReducers} from 'redux';


const reducers = combineReducers({
  alcohols: alcoholReducer,
  cocktails: cocktailReducer
})

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
let store = createStore(reducers, composeEnhancers(applyMiddleware(thunk)))

```

What a simple solution to such a complex issue I was having. It was working through these issues I came to find out how many different things react/ redux can do and how many items have already been built into the platform. 

I hope to continue my studies with this platform and get more comfortable as my career search starts. 

But I am proud of myself, I made it through a pandemic, and learned a new skill along the way. 
