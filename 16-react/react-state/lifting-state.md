# Lifting State

## ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Unidirectional Data Flow

#### Learning Objectives

_After this lesson, you will be able to:_

* Define unidirectional flow
* Diagram data in a component hierarchy

### What is Unidirectional Data Flow?

Let's start with [a video explaining this concept.](https://generalassembly.wistia.com/medias/v2uenqkgwk).

In React applications, data usually flows from the top down. Why do we care? How does this apply?

When several components in a view need to share `state`, you lift, or **hoist**, the `state` so that it's available to all the components that need it. Define the state in the highest component you can, so that you can pass it to any components which will need it. Let's look at a search filter as an example. This app will have two basic components - one that displays a list of data, and one that captures user input to filter the data.

Download Mateens react simple starter :
`git clone https://github.com/MateenCode/Simple-React-Starter`
and `cd` into `Simple-React-Starter`
run `code .` to open vs code and `npm i` followed by `npm start` to get the sever started
We will  be working with functional components. Lets remove reference to Class based components.
Lets update our App.js to look like this.
```
import React, { Component } from "react";
// Components imports
import FunctionalComponent from "./components/FunctionalComponent";
// CSS imports
import "./css/App.css";
class App extends Component {
  render() {
    return (
      <div className="App">
        <FunctionalComponent />
      </div>
    );
  }
}
export default App;
```
and lets delete the ClassComponent in the /src/components folder.
Now lets add some state to app at the inside of out app component app.js
`  state = { playerName: "YOUR NAME" };`
Lets also display that name under out Functional component.
Our App component should now look like this
```
class App extends Component {
  state = {
    playerName: "Billie"
  }
  render() {
    return (
      <div className="App">
        <FunctionalComponent />
        {this.state.playerName}
      </div>
    );
  }
}
```
Now lets make our first component.
in your components folder lets make a file name PlayerDetails.js
(You can check which directory you are in by running `pwd`)
`touch src/components/PlayerDetails.js`
Lets open this file and define a functional component. It will take props ( a name ) and return that name in a div.
Should looke like this.
```
import React from 'react'
const PlayerDetails = ({playerName}) => {
    return (
        <div>
            {playerName}
        </div>
    )
}
export default PlayerDetails
```
Now lets import this into out App.js and pass the name from state into our new PlayerDetail component
Your updated App component should look like this
```
class App extends Component {
  state = {
    playerName: "Billie"
  }
  render() {
    return (
      <div className="App">
        <FunctionalComponent />
        <PlayerDetails playerName={this.state.playerName}/>
      </div>
    );
  }
}
```
Now lets make two components to display buttons to toggle Which Player to display.
Just like the PlayerDetails components, in the src/components folder lets make a new file named `PlayerContent.js`
in this file lets define a functional component which takes props ( an id and a playerName ). This component will contain a button which displays the playerName. and a onclick handler which for now will alert which player we clicked.
It should look like this.
```
const PlayerConent = ({playerName, id}) => {
    return (
        <div>
            <button
                onClick={()=>{
                    alert(playerName)
                }}
            >
                {playerName}
            </button>
        </div>
    )
}
export default PlayerConent
```
Lets import this into our app.js and have two instances of this component and lets pass a playerName and an id for each box.
App.js should look like this.
```
class App extends Component {
  state = {
    playerName: "Billie"
  }
  render() {
    return (
      <div className="App">
        <FunctionalComponent />
        <PlayerContent
          playerName="Billie"
          id={0}
        />
        <PlayerContent
          playerName="Mateen"
          id={1}
        />
        <PlayerDetails playerName={this.state.playerName}/>
      </div>
    );
  }
}
```
Now, If we want to update the name being displayed how would we do that?
===============================================================


In our App.js Lets make handler which will take id and name and set the state based params id, and playerName.
and lets now pass that to our Player Content components through the clickHandler
Should looke something like this
```
class App extends Component {
  state = {
    playerName: "Billie"
  }
  updateSelectedPlayer = (playerName) => {
    this.setState({
      playerName: playerName,
    });
  };
  render() {
    return (
      <div className="App">
        <FunctionalComponent />
        <PlayerContent
          updateSelectedPlayer={this.updateSelectedPlayer}
          playerName="Billie"
          id={0}
        />
        <PlayerContent
          updateSelectedPlayer={this.updateSelectedPlayer}
          playerName="Mateen"
          id={1}
        />
        <PlayerDetails playerName={this.state.playerName}/>
      </div>
    );
  }
}
```
Now last lets pass updateSelectedPlayer to our PlayerContent and call is with playerName.

Our updated PlayerContent should looke like this
```
const PlayerContent = ({playerName, id, updateSelectedPlayer}) => {
    return (
        <div>
            <button
                onClick={()=>{
                    updateSelectedPlayer(playerName)
                }
            }
            >
                {playerName + id}
            </button>
        </div>
    )
}
```

Now when we click each button we should see the name updating from Mateen to Billie.

Extra practice.
Try using the id prop to toggle the buttons color based on the buttons id.


## extra links
https://reactjs.org/docs/lifting-state-up.html
