#### Trello: as a user I can view a list of instructions to help me brew my coffee.

Our final component is the instructions box which is the list of instructions for each brew method.
This simple component is made using a bootstrap component, the Carousel.

We made a few adjustments to it just because we're dealing with texts and not images.

First, as usual we'll go to our `Components` folder and make a new folder called `Instructions` and create an `index.js` file.


```
import React from "react";

//Styling
import "../../style.css";

const Instructions = ({ brewingMethod }) => {
  const instructions = brewingMethod.instructions;
  let count = 0;

  const instructionList = instructions.map(inst => {
    if (count === 0) {
      count += 1;

      return (
        <div className="carousel-item active">
          Step: {count} <br />
          <br />
          {instructions[0]}
        </div>
      );
    } else {
      count += 1;
      return (
        <div className="carousel-item">
          Step: {count} <br />
          <br />
          {inst}
        </div>
      );
    }
  });
  return (
    <div
      id="carouselControls"
      className="carousel slide"
      data-ride="carousel"
      data-interval="false"
    >
      <div className="carousel-inner">
        <div className="card-body">
          <p className="card-text">{instructionList}</p>
        </div>
      </div>

      <button
        className="carousel-control-next"
        href="#carouselControls"
        role="button"
        data-slide="next"
        style={{
          height: "165px",
          width: "15px",
          color: "black"
        }}
      >
        >
        <span className="carousel-control-next-icon" aria-hidden="true"></span>
        <span className="sr-only">Next</span>
      </button>
    </div>
  );
};
export default Instructions;
```

first we mapped over the instruction list array given in the `data.js` file.
Next we take the first element in the array and return it with the class `carousel-item active` and increase the counter, so that all other elements will be returned with the class `carousel-item`.

the count variable is as it's called, counts the number of instructions so we can display them as steps for the user.

finally we placed the mapped array `instructionList` as the card text/body to actually display the instructions.

to display this we're going to add it under the `Timer` component in `BrewingMethodModal` within a `div` for styling purposes

```
const BrewingMethodModal = ({ brewingMethod, handleToggle, modalState }) => {
  return (
    <Modal size="lg" isOpen={modalState} toggle={handleToggle}>
      <ModalHeader toggle={handleToggle}>{brewingMethod.name}</ModalHeader>
      <ModalBody>
        <AmountCalculator brewingMethod={brewingMethod} />
        <div className="wrapper-details-inst">
          <Timer brewingMethod={brewingMethod} />
          <Instructions brewingMethod={brewingMethod} />
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
```

dont' forget to import it at the top!
and for the last time `add`, `commit` and `push` and move your last card to `Done`!
and that's all folks!!
