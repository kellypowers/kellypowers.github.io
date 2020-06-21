---
layout: post
title:      "React- Redux Final Project"
date:       2020-06-21 20:56:07 +0000
permalink:  react-_redux_final_project
---


My final project is a web application that uses the Smite API to look up information for the game Smite.
For those who have never heard of Smite, it is a MOBA (Multiplayer Online Battleground Arena) game that uses different gods as characters, and players fight on different battleground maps.  My friends and I have played this game for many years, and during the pandemic we have played a lot as our only social activity, so I thought building an app that allows us to look up our games and stats would be a fun thing to build.

React is a JS library that makes building user interfaces much easier and faster than regular JS, such as my last project, where DOM elements had to be added and removed individually.  With React, components are created and can be reused over and over.  React uses JSX which allows us to use Javascript directly into our HTML elements rather than keep the HTML and JS seperate.  Using JSX, within an HTML element, a JavaScript expression is written inside curly braces.  A new react appication uses the CLI command:
```
create-react-app
```
which creates a bare react application that includes all the packages you would need for a basic react app.

React uses components to render HTML elements to the page.  A Class Component can have it's own state.  A Functional Component can only have state through the use of hooks.  A Presentational component is a small component used to only display an HTML element.

Redux is middleware for React that makes it easy to manage state for the application.  The application state for my app is comprised of Gods, Builds, Items, Players and Player Matches.  The Redux Store is the application's state, and this is connected to components using the react-redux connect feature.  Redux connects state to props in components using mapStateToProps, and dispatches actions to create a new state (state of the appplication should not change, but instead changes are made by copying the old state and adding/deleting elements, and returning a NEW state).  
```
import { connect } from 'react-redux


const mapStateToProps = state => {
  return {
    gods: state.gods,
    items: state.items,
    loading: state.loading
  }
}


const mapDispatchToProps = dispatch => {
    return {
        removeGod: id => dispatch({type: "REMOVE_GOD", id})
    }
}

export default connect(mapStateToProps, mapDispatchToProps)(GodsContainer)
```



My backend is a Rails API backend, and my database has tables for Gods and Items, which were created from fetching this information from the Smite API and seeded into my database tables.  My frontend has an option to create builds for gods, which is persisted to my backend database for God Builds.  My application allows to search for players, and this communicates to the backend, which in turn creates a session to the Smite API an returns the information from the Smite API.
