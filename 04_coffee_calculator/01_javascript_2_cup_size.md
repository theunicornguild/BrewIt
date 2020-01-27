#### Trello: as a user I can select the cup size of my coffee mug.

Before we start anything lets move the trello card from `Backlog-To-do` to `Doing`.

Now the fun begins, let's create our component the same way we usually do by first creating a folder in the Component's folder and call it `CupSize` and then make a new file called `index.js`

In this component we'll have three buttons representing the three standard coffee cup sizes which are 
- 8oz(227ml)
- 12oz(240ml)
- 16oz(454ml).

`src/Components/CupSize/index.js`

```
import React from "react";

//Styling
import "../../style.css";
import "../../Modal.css";

const CupSize = () => {
  return (
    <div className="wrapper-details">
      <h5 className="text-center mt-4">Cup Size:</h5>
      <button className="cup-box">8oz</button>
      <button className="cup-box">12oz</button>
      <button className="cup-box">16oz</button>
    </div>
  );
};
export default CupSize;
```


Now to view it on the page let's import it in the `BrewingMethodModal/index.js` and place it under the **BrewingMethodDetails** components in the body.

```
import React from "react";
//Components
import { Modal, ModalHeader, ModalBody, ModalFooter } from "reactstrap";
import BrewingMethodDetails from "../BrewingMethodDetails/index";
import CupSize from "../CupSize/index";

//Styling
import "../../style.css";
import "../../Modal.css";

const BrewingMethodModal = ({ brewingMethod, handleToggle, modalState }) => {
  return (
    <Modal size="lg" isOpen={modalState} toggle={handleToggle}>
      <ModalHeader toggle={handleToggle}>{brewingMethod.name}</ModalHeader>
      <ModalBody>
        <BrewingMethodDetails brewingMethod={brewingMethod} />
        <CupSize />
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
