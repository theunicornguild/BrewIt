Trello: I can then see details of that specific brewing method.

Now that we have our 'base' we can add all the information and additional components that will help the user brew their coffee!

First let display some information about the brewing method on the modal with some of the data provided in the data.js file.

In your BrewingMethodModal/index.js file let's add brewingMethod as a prop so we can access the information for each brewing method.

let's add the name in the modal header and grind size, total_time, grams of coffee and the water amount in the modal body.
As mentioned earlier all styling is already provided.


import React from "react";
//Components
import { Modal, ModalHeader, ModalBody, ModalFooter } from "reactstrap";

//Styling
import "../../style.css";
import "../../Modal.css";

const BrewingMethodModal = ({ brewingMethod, handleToggle, modalState }) => {
  return (
    <Modal size="lg" isOpen={modalState} toggle={handleToggle}>
      <ModalHeader toggle={handleToggle}>{brewingMethod.name}</ModalHeader>
      <ModalBody>
        <div className="wrapper-details">
          <div className="modal-box">
            <div>Grind Size: </div> <br />
            <div>{brewingMethod.grind_size}</div>
          </div>
          <div className="modal-box">
            <div>Brew Time:</div> <br />
            <div> {brewingMethod.total_time} minutes</div>
          </div>
          <div className="modal-box">
            <div>Grams of Coffee:</div> <br />
            <div> {brewingMethod.default_grams}g</div>
          </div>
          <div className="modal-box">
            <div>Water:</div> <br />
            <div> {brewingMethod.default_water}ml</div>
          </div>
        </div>
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


To make things easier for ourselves later on let's put these details in their own component.
In the components folder make a new folder called 'BrewingMethodDetails' and in that make an index.js file and paste the details we just wrote and of course don't forget to pass the props.

BrewingMethodDetails/index.js

import React from "react";

//Styling
import "../../style.css";

const BrewingMethodDetails = ({ brewingMethod }) => {
  return (
    <div className="wrapper-details">
      <div className="modal-box">
        <div>Grind Size: </div> <br />
        <div>{brewingMethod.grind_size}</div>
      </div>
      <div className="modal-box">
        <div>Brew Time:</div> <br />
        <div> {brewingMethod.total_time} minutes</div>
      </div>
      <div className="modal-box">
        <div>Grams of Coffee:</div> <br />
        <div> {brewingMethod.default_grams}g</div>
      </div>
      <div className="modal-box">
        <div>Water:</div> <br />
        <div> {brewingMethod.default_water}ml</div>
      </div>
    </div>
  );
};
export default BrewingMethodDetails;


and now let's remove all that code from the BrewingMethodModal file and just render that componet instead.

import React from "react";
//Components
import { Modal, ModalHeader, ModalBody, ModalFooter } from "reactstrap";
import BrewingMethodDetails from "../BrewingMethodDetails/index";
//Styling
import "../../style.css";
import "../../Modal.css";
const BrewingMethodModal = ({ brewingMethod, handleToggle, modalState }) => {
  return (
    <Modal size="lg" isOpen={modalState} toggle={handleToggle}>
      <ModalHeader toggle={handleToggle}>{brewingMethod.name}</ModalHeader>
      <ModalBody>
        <BrewingMethodDetails brewingMethod={brewingMethod} />
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



that's it! now in the next chapters we'll create some components that will help the user adjust their coffee based on their preference.
