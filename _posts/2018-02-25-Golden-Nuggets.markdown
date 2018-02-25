---
layout: post
title: Golden Nuggets
date: 2018-02-25 17:50:39-05:00
categories: psychology, turning pro, motivation
---

# Why We Work

Of course, it's because our Soul tells us to.  And it doesn't pay to fool with the Soul.  But along the way, there are moments when we strike gold.  And I'm talking about personal gold here, not necessarily huge payoffs from other resources, like royalty checks and guest spots on Late Night or SNL.  I'm talking about those personal wins that make you feel like a million dollars.

I'm a programmer and writer.  (I think there's another one I'm forgetting, like Daddy, but just keeping up with these two is plenty for the moment.)  So when I write a program, most of the time the program is broken.  Most of the time I'm trying to fix something that is wrong with it.  With my current project, I've been working on it for months, and just getting some small parts to work are what I depend on for my happy dance.  But today, I did a big happy dance.

# User Auth

I'm working with the MERN stack (MongoDB, ExpressJS, ReactJS, and NodeJS).  I have gotten the app up and running from a static client perspective.  Then I got the API mostly working.  And this last week I've been working on getting the user auth system working.  And today I finally got the user's profile page to render, once he was logged in.  I had been working all weekend on that.  So YAY!

This was my first time doing something like the following in my store:
```
// Hydrate the authToken from localStorage if it exists
const authToken = loadAuthToken();

const store = createStore(
  combineReducers({
    reducer,
    form: formReducer,
    auth: authReducer,
    protectedData: protectedDataReducer
  }),
  applyMiddleware(thunk)
);

if (authToken) {
  const token = authToken;
  store.dispatch(setAuthToken(token));
  store.dispatch(refreshAuthToken());
  console.log("In the Store--token: ",token);
}
```
I actually borrowed this from the Thinkful curriculum, but I did need to include my pre-existing reducer.  I included this in the first line of the combineReducers() method, after importing it earlier in the file.

Of course, there're still many tons of info left for me to work on, but this was when things started to change.  This is what unified all of my reducers into a single store that can provide the rest of the app with data.  It doesn't look like much, but using it today was a seminal moment!

# Happy Dance

Some days there's not a happy dance to be had anywhere.  You simply sit down and put in the work, knowing that today was no payday.  You just grunt through the day, hoping that tomorrow will yield something for you.  

This is tough.  So, I think there should be at least two times when you deserve a happy dance: 

1. when you actually get a payoff, like today for me, and 

2. when you put in your time and beat _Resistance_.

So maybe I should do _two_ happy dances today?