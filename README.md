# Awesome-Learning-For-Awesome-Devs-
A repo for learn@work knowledge

## Day 4 (November 13, 2017)
Wes Bos - Learn Redux Course

### Testing Suite
Start by running the following commands in your dev environment. We will use these modules in the coming days to start testing our react components. 

npm install --save-dev jasmine-enzyme@2.1.2

npm install --save-dev enzyme@2.7.1

npm install --save-dev jasmine@2.4.1

As we move forward, please familiarize yourself with the following docs. 
https://github.com/airbnb/enzyme/tree/v2.7.1/docs

https://jasmine.github.io/2.4/introduction

### Actions and action creators
Actions are payloads of information that send data from your application to your store. They are the only source of information for the store.
```
{
    type: "ADD_COMMENT",
    postId,
    author,
    comment
}
```
Actions are plain JavaScript objects. Actions must have a type property that indicates the type of action being performed.

Action creators are functions which purpose is to create and return an action with a type and a payload.
```
function addComment(postId, author, comment) {
  return {
    type: "ADD_COMMENT",
    postId,
    author,
    comment
  };
}
```
Other than type, the structure of an action object is really up to you.

Read more:
https://redux.js.org/docs/basics/Actions.html

#### Next Step: Defining reducers
We will be learning how to set up reducers to specify how the state updates when you dispatch actions.  If you want to get a head start you can read the docs on Reducers here: https://redux.js.org/docs/basics/Reducers.html


## Day 3 (November 6. 2017)
Wes Bos - Learn Redux Course
### App Layout + Component Setup
* Setup Main, PhotoGrid, and Single components that will be used for the Reduxstagram app.

### Setting up React Router
* Imported react-router and imported all components into reduxstagram.js file.
* Setup basic router configuration using Router, Route, IndexRouter, and browserHistory from react-router.
```
import React from 'react';

import { render } from 'react-dom';

// Import css
import css from './styles/style.styl';

// Import Components
import Main from './components/Main';
import Single from './components/Single';
import PhotoGrid from './components/PhotoGrid';

// import react router deps
import { Router, Route, IndexRoute, browserHistory } from 'react-router';

const router = (
  <Router history={browserHistory}>
    <Route path="/" component={Main}>
      <IndexRoute component={PhotoGrid}></IndexRoute>
      <Route path="/view/:postId" component={Single}></Route>
    </Route>
  </Router>
)

render(router, document.getElementById('root'));
```

## Day 2 (October 30, 2017)
Decided as a team to switch from Tyler McGinnis to Wes Bos, Learn Redux course, https://learnredux.com/

### Wes Bos: Learn Redux
* We cloned the start files and setup the basic webpack environment.

## Day 1 (October 23, 2017)

### REDUX: a predictable state container for JavaScript apps.

What are the benefits of Redux?
* Provides an easier way to share data between components
* Provides an enhanced dev experience through Hot Module Replacement and Redux Dev Tools
* Makes testing easier, mostly because it facilitates the use of pure functional React components.
* Helps manage state in your application 
* View the entire state of your application at once since it’s all in a single state store / tree

### FIREBASE: A real-time, cloud-hosted database. Data is stored as JSON and synchronized in real-time to every connected client.

#### Two Rules for Schema

* Keep your data shallow (firebase can only query one node at a time)
* Don’t be afraid of duplicating data (to create faster reads)

Imagine the following data =>
```
users: {
    tylermcginis: {
        name: 'Tyler McGinnis',
        age: 25,
        posts: {
            post1: {
                title: 'What is a jQuery',
                date: 1461131626103,
                likes: {
                    'jakelingwall': true,
                    'eanplatter': true,
                    'mikenzi': true
                },
                replies: {
                    reply1: {
                        name: 'Jake Lingwall',
                        comment: 'Its a monad',
                        id: 'jakelingwall'
                    },
                    reply2: {
                        name: 'Ean Platter',
                        comment: 'Its a type of Java',
                        id: 'eanplatter'
                    }
                }
            }
        }
    }
}
```
To follow our rules of keeping data shallow and not fearing duplication in the hunt for faster reads, we would refactor to this =>
```
users: {
    tylermcginis: {
        name: 'Tyler McGinnis',
        age: 25,
        posts: {
            post1: true,
        }
    }
},
posts: {
    post1:{
        title: 'What is a jQuery',
        date: 1461131626103,
        likes: {
            'jakelingwall': true,
            'eanplatter': true,
            'mikenzi': true
        },
        replies: {
            post1: {
                reply1: {
                    name: 'Jake Lingwall',
                    comment: 'Its a monad',
                    id: 'jakelingwall'
                },
                reply2: {
                    name: 'Ean Platter',
                    comment: 'Its a type of Java',
                    id: 'eanplatter'
                }
            }
        },
    }
}
```
#### Query Methods
If my main project was called “Uber for Dogs”, my project (and data) would live at https://uber-for-dogs.firebaseio.com/
If I then POSTed to that url with this object 
```
{
  name: 'Wendy Moira Angelou'
}
```
Then navigated to https://uber-for-dogs.firebaseio.com/name
It would return 'Wendy Moira Angelou'

#### Project Specific Firebase Schema
```
/users
  uid
    name
    uid
    avatar

/ducks
  duckId
    avatar
    duckId
    name
    text
    timestamp
    uid (of duck author)

/likeCount
  duckId
    0

/usersDucks
  uid
    duckId
      avatar
      duckId
      name
      text
      timestamp
      uid (of duck author)

/replies
  duckId
    replyId
      name
      comment
      uid
      timestamp
      avatar

/usersLikes
  uid
    duckId: true
```
#### Homework
If you want to achieve the level of Super Duper Awesome Dev™, read https://howtofirebase.com/firebase-data-modeling-939585ade7f4

