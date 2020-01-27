#### Trello: I can then select the coffee to water ratio.

Our buttons currently don't really do anything that's because we need one more component to start connecting everything together and do our calculations.

and that component will be a number slider that we will import from `material-ui`.

the slider will help determine how 'strong' or 'light' the coffee will be.

let's make a new folder in the component's folder and call it `AmountCalculator` and create an `index.js` file.

first let's import the slider.

`src/Components/AmountCalculator/index.js`
```
import React from "react";

//Components
import Slider from "@material-ui/core/Slider";

//Styling
import "../../style.css";

const AmountCalculator = () => {
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

  const handleRatio = value => {
    return JSON.stringify(value);
  };

  return (
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
  );
};
export default AmountCalculator;
```

The `marks` variable is an array to store the values of the slider to be displayed and also that we will use later for the calculation.
and the `handleRatio` function just returns those values as a string. 
so again so far this only displays the value but doesn't affect anything, so let's put the `CupSize` component and the `BrewingMethodDetails` in this `AmountCalculator/index.js` file.

and put the `AmountCalculator` component in the `BrewingMethodModal/index.js` file to make things easier for later.

don't forget to pass the **brewingMethod** as props.

```
import React from "react";
//Components
import { Modal, ModalHeader, ModalBody, ModalFooter } from "reactstrap";
import AmountCalculator from "../AmountCalculator/index";

//Styling
import "../../style.css";
import "../../Modal.css";

const BrewingMethodModal = ({ brewingMethod, handleToggle, modalState }) => {
  return (
    <Modal size="lg" isOpen={modalState} toggle={handleToggle}>
      <ModalHeader toggle={handleToggle}>{brewingMethod.name}</ModalHeader>
      <ModalBody>
        <AmountCalculator brewingMethod={brewingMethod} />
      </ModalBody>
      <ModalFooter>
        <button className="button button-dark" onClick={handleToggle}>
          Cancel
        </button>
      </ModalFooter>
    </Modal>
  );
};
export default BrewingMethodModal;
```


**src/Components/AmountCalculator/index.js**

```
import React from "react";

//Components
import Slider from "@material-ui/core/Slider";
import BrewingMethodDetails from "../BrewingMethodDetails/index";
import CupSize from "../CupSize/index";

//Styling
import "../../style.css";

const AmountCalculator = ({ brewingMethod }) => {
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

  const handleRatio = value => {
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
      <CupSize />
      <hr className="mt-2 mb-4" />

      <BrewingMethodDetails brewingMethod={brewingMethod} />
    </div>
  );
};
export default AmountCalculator;
```
