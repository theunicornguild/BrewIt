	Trello card: As a user I can see a list of brewing methods.

Before we begin, move the current trello card from the `Backlog/To-do` to `Doing` so we can keep track of which component we're working on.

After cloning the project and installing the packages you can see that there’s some code written for you as a starter which includes all the css and styling as well.

You will also have a  `src/data.js` file.
This file contains all of the brewing methods’ information that we will display and use later on.


We’ll first begin by displaying the brewing methods’ names and images that we’ll import from the `src/data.js` file.
To do this we have to map through the array of objects which we have stored as a state as ‘brewingMethods’.

Your `src/App.js` file should look something like this:

```
import React, { useState } from "react";
import "./App.css";

import allBrewMethods from "./data";

function App() {
  const [brewingMethods] = useState(allBrewMethods);

  const methodList = brewingMethods.map(method => (
    <div className="col-4">
      <h3>{method.name}</h3>
      <img src={method.imageUrl} alt={method.name} className="mx-auto" />
    </div>
  ));

  return (
    <div className="App my-5">
      <div className="container">
        <div className="row">{methodList}</div>
      </div>
    </div>
  );
}

export default App;
```
