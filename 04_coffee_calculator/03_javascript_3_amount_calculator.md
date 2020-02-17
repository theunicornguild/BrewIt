
we've now done two of our main components and combined them in one component which is `AmountCalculator` but it still doesn't change any values.

we're going to add all the functions and pass all the props required to make our component more useful.

First we'll add a few states,

- one for the slider component amount,the ratio (amount).
- one to set the coffee grams amount based on the calculation(grams).
- another one for the water amount for the coffee(water).
- the last one to store the value from the component CupSize which will be initalized to 227 as a default(selectedOption).

```
  const [amount, setAmount] = useState();
  const [grams, setGrams] = useState();
  const [water, setWater] = useState();
  const [selectedOption, setSelectedOption] = useState(227);
```

Now in our slider component we already have the `handleRatio` function being used there to simply return the value as a string. We'll add to the function so that it will also set the state.

```
    const handleRatio = value => {
    setAmount(value);
    return JSON.stringify(value);
  };
```

Another thing we'll need is a function that we'll call `handleChange`. Which will do our main calculation for the coffee grams and water amount.

the general equation is (cupsize/ratio amount) \* 15.

```
   const handleChange = () => {
    setGrams(parseInt(selectedOption / amount));
    setWater(parseInt(grams * 15));
  };
```

and finally we'll put `handleChange` in `handleRatio` so it would call it whenever the user chooses another value from the slider.

```
    const handleRatio = value => {
    setAmount(value);
    handleChange();
    return JSON.stringify(value);
  };
```

Before switching to the `CupSize` component let's first send some props to it.
Add `handleChange`, `selectedOption` and `setSelectedOption`.

```
   <CupSize
        handleChange={handleChange}
        selectedOption={selectedOption}
        setSelectedOption={setSelectedOption}
      />
```

Now going over to `CupSize` and use these props to store our value.
first we'll need another function to store the value on an `onClick` for each cup size(button) of the selected size in ml.

```
  const handleChoice = e => {
    setSelectedOption(e);
    handleChange(selectedOption);
  };
```

so the whole thing will look something like this.

**src/Components/CupSize/index.js**

```
  import React from "react";

//Styling
import "../../style.css";
import "../../Modal.css";

const CupSize = ({ handleChange, selectedOption, setSelectedOption }) => {
  const handleChoice = e => {
    setSelectedOption(e);
    handleChange(selectedOption);
  };
  return (
    <div className="wrapper-details">
      <h5 className="text-center mt-4">Cup Size:</h5>
      <button className="cup-box" onClick={() => handleChoice(227)}>
        8oz
      </button>
      <button className="cup-box" onClick={() => handleChoice(240)}>
        12oz
      </button>
      <button className="cup-box" onClick={() => handleChoice(454)}>
        16oz
      </button>
    </div>
  );
};
export default CupSize;
```

Going back to to the `AmountCalculator` component the last thing we need to do here is pass the `grams` and `water` value to **BrewingMethodDetails** so it will change based on the user's choices. so this will be the finished code.

**src/Components/AmountCalculator/index.js**

```
import React, { useState } from "react";

//Components
import Slider from "@material-ui/core/Slider";
import BrewingMethodDetails from "../BrewingMethodDetails/index";
import CupSize from "../CupSize/index";

//Styling
import "../../style.css";

const AmountCalculator = ({ brewingMethod }) => {
  const [amount, setAmount] = useState();
  const [grams, setGrams] = useState();
  const [water, setWater] = useState();
  const [selectedOption, setSelectedOption] = useState(227);

  const marks = [
    {
      value: 12,
      label: "12"
    },
    {
      value: 13,
      label: "13"
    },
    {
      value: 14,
      label: "14"
    },
    {
      value: 15,
      label: "15"
    }
  ];
  const handleChange = () => {
    setGrams(parseInt(selectedOption / amount));
    setWater(parseInt(grams * 15));
  };

  const handleRatio = value => {
    setAmount(value);
    handleChange();
    return JSON.stringify(value);
  };

  return (
    <div>
      <div className="wrapper-details-input">
        <div>
          <h5 className="text-center">Coffee to Water Ratio: </h5>
        </div>
        <div>
          <h6 className="text-center">stronger</h6>
        </div>
        <Slider
          orientation="horizontal"
          defaultValue={15}
          min={12}
          max={15}
          getAriaValueText={handleRatio}
          step={1}
          marks={marks}
          valueLabelDisplay="on"
          style={{
            width: "200px",
            color: "#8cb9fd"
          }}
        />
        <div>
          <h6 className="text-center">lighter</h6>
        </div>
      </div>
      <hr className="mt-2 mb-4" />
      <CupSize
        handleChange={handleChange}
        selectedOption={selectedOption}
        setSelectedOption={setSelectedOption}
      />
      <hr className="mt-2 mb-4" />

      <BrewingMethodDetails
        brewingMethod={brewingMethod}
        grams={grams}
        water={water}
      />
    </div>
  );
};
export default AmountCalculator;
```

and now you made your own basic coffee calculator!

you can now move both trello cards to `Done` and git `add`, `commit` and `push` your code!

