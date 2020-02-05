After all thats done we want to apply some styling to each method to make it look more presentable.
To do that I have included all the styling necessary but we will need to make another file for each brewing method item.

In the `BrewingList` folder make a new file called `BrewMethodItem.js`

and let's add the details that we need to display for each method, the `src/Components/BrewingList/BrewMethodItem.js` file should look like this.

//Mariam: wrong import "../../style.css" in both BrewingList and BrewMethodItem

```
import React from "react";

// Styling
import "../style.css";

const BrewMethodItem = ({ brewingMethod }) => {
  return (
    <div>
      <h3 className="font-weight-medium text-center text-lg-left mt-4 mb-0">
        {brewingMethod.name}
      </h3>
      <hr className="mt-2 mb-5" />
      <div className="row text-center text-lg-left">
        <div className="box">
          <img
            className="img-fluid img-thumbnail"
            src={brewingMethod.imageUrl}
            alt={brewingMethod.name}
            style={{ height: 160, width: 170 }}
          />
          <div>
            <button className="btn">Brew</button>
          </div>
        </div>
      </div>
    </div>
  );
};
export default BrewMethodItem;
```

//Mariam: wrong path -> missing /Components
We should then alter the `src/BrewingList/index.js` file to use the `BrewMethodItem` component.

```
import React from "react";

//Components
import BrewMethodItem from "./BrewMethodItem";

//Styling
import "../style.css";

const BrewingList = ({ brewingMethods }) => {
  const methodList = brewingMethods.map(method => (
    <div className="col-4">
      <BrewMethodItem brewingMethod={method} />
    </div>
  ));

  return <div className="row">{methodList}</div>;
};

export default BrewingList;
```

//Mariam: add a key to the brewingList for each item
Now you can finally move the 'As a user I can see a list of brewing methods.' card in trello from `doing` to `done`!
and then in your terminal git `add`, `commit` and `push` your code to your repo.
