To make our code cleaner and tidier, we need to move the code we wrote in the `App.js` file into its own component.
In your projects folder you will see a folder called `Components`.
Make another folder inside it called `BrewingList`.

Inside this folder create a new file called `index.js` and place the code that we wrote in the `App.js` so it would look something like this.

`src/Components/BrewingList/index.js`

```
import React from "react";

const BrewingList = ({ brewingMethods }) => {
  const methodList = brewingMethods.map(method => (
    <div className="col-4">
      <h3>{method.name}</h3>
      <img src={method.imageUrl} alt={method.name} className="mx-auto" />
    </div>
  ));

  return <div className="row">{methodList}</div>;
};

export default BrewingList;
```

After that we should call this component in `App.js` to render it there and pass it the necessary props.
replace the `'null'` written in the `showHome` condition:

`{showHome ? (null) : (<AboutPage />)}`

with the `BrewingList` component.

`<BrewingList brewingMethods={brewingMethods} />`



```
import React, { useState } from "react";

//Style
import "./App.css";

//Data
import allBrewMethods from "./data";

//Components
import BrewingList from "./Components/BrewingList/index.js";
import AboutPage from "./Components/AboutPage";
import NavBar from "./Components/NavBar";

function App() {
  const [brewingMethods] = useState(allBrewMethods);
  const [showHome, setShowHome] = useState(true);


  return (
    <>
    <NavBar setShowHome={setShowHome} />
      <div className="App my-5">
        <div className="container">
          {showHome ? (
            <BrewingList brewingMethods={brewingMethods} />
          ) : (
            <AboutPage />
          )}
        </div>
      </div>
    </>
  );
}
export default App;
```
`src/App.js`
