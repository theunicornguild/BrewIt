#### Trello: as a user I can see a pop-up window when I click on a brewing method.

As you can see, we already have a button included in the `BrewMethodItem.js` component but it currently doesn't do anything. So let's make it more useful by having a pop-up window appear with all the details of the specified method once we click on it.

In the components folder create a new folder called BrewingMethodModal and in that folder we'll create a file and name it `index.js`

We'll be using a Modal template from `reactstrap` which should be already installed as a package in your starter file. So we'll need to import a few things from it so your `BrewingMethodModal/index.js` will be something like this.

```
import React from "react";
//Components
import { Modal, ModalHeader, ModalBody, ModalFooter } from "reactstrap";
//Styling
import "../../Modal.css"

const BrewingMethodModal = ({ handleToggle, modalState }) => {
  return (
    <Modal size="lg" isOpen={modalState} toggle={handleToggle} backdrop="false">
      <ModalHeader toggle={handleToggle}></ModalHeader>
      <ModalBody>
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

This will still won't do anything yet because we have to associate the modal with our `button` that we have in the `BrewingList/BrewMethodItem.js` file and with that we will also pass some props to control the state of the modal.

In the `BrewingList/BrewMethodItem.js` file we'll add the modal state which will store the 'state' of the modal (opened or closed) and a function that will handle this event as well.
Finally we'll link the button as well as the entire component to the modal so that when the user clicks on a brewing method the pop-up window will come up.

Now lets add all these changes to `BrewingList/BrewMethodItem.js`

```
import React, { useState } from "react";

//Component
import BrewingMethodModal from "../BrewingMethodModal/index";
// Styling
import "../../style.css";
import "../../Modal.css";

const BrewMethodItem = ({ brewingMethod }) => {
  const [modalState, setModalState] = useState(false);

  const handleToggle = () => {
    setModalState(!modalState);
  };

  return (
    <div onClick={handleToggle}>
      <h3 className="font-weight-medium text-center text-lg-left mt-4 mb-0">
        {brewingMethod.name}
      </h3>
      <hr className="mt-2 mb-4" />
      <div className="row text-center text-lg-left">
        <div className="box">
          <img
            className="img-fluid img-thumbnail"
            src={brewingMethod.imageUrl}
            alt={brewingMethod.name}
            style={{ height: 160, width: 170 }}
          />
          <div>
            <button
              id="#btn"
              type="button"
              className="btn"
              data-toggle="modal"
              data-target="#brewingModal"
            >
              Brew
            </button>
          </div>

          <BrewingMethodModal
            handleToggle={handleToggle}
            brewingMethod={brewingMethod}
            modalState={modalState}
          />
        </div>

      </div>
    </div>
  );
};
export default BrewMethodItem;
```
congratualtions now you have a pop-up modal!
You can move your trello card from `doing` to `done`!
