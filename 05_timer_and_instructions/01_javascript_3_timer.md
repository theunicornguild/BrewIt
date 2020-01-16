#### Trello: I can then start the timer once I start making my coffee.

Finally we're going to build a fun little component that will help the user while brewing their coffee which is a timer!

Let's begin by going to our dear Component folder and make a folder called Timer and have an `index.js` file.

we'll start by creating the basic structure of our component which will be the Start and Reset buttons and the section where the time itself will be displayed.

As mentioned previously all styling has been already provided in the starter file so we'll just import it.
```
import React from "react";

//Styling
import "../../timer.css";

const Timer = () => {
  return (
    <div className="app">
      <div className="time">s</div>
      <div className="row">
        <button className="button-primary">Start</button>
        <button className="button-secondary">Reset</button>
      </div>
    </div>
  );
};

export default Timer;
```

To view this, let's call this component in our `BrewingMethodModal` and place it under the `AmountCalculator` component. Let's also pass **brewingMethod** as a prop so we can use it for an extra feature later.

`<Timer brewingMethod={brewingMethod} />`

Now let's create our states which are Seconds, Minutes which will store the value of the timer and `isActive` which will have the timer's state to check whether it's active or paused.

(don't forget to import useState at the top).
```
  const [seconds, setSeconds] = useState(0);
  const [minutes, setMinutes] = useState(0);

  const [isActive, setIsActive] = useState(false);
```
  we initialized the `seconds` and `minutes` to zero and the `isActive` state is false as in paused.

  Now let's incorporate our states into the code we wrote earlier to change the component based on the current state.
```
  return (
    <div className="app">
      <div className="time">
        {minutes}mins:{seconds}s
      </div>
      <div className="row">
        <button
          className={`button button-primary button-secondary-${
            isActive ? "active" : "inactive"
          }`}
        >
          {isActive ? "Pause" : "Start"}
        </button>
        <button className="button btn-danger">Reset</button>
      </div>
    </div>
  );
```
  now that we have our basic structure let's make this timer actually work.
  let's start by adding an `onClick` for the first button to set the state for starting/pausing the timer.
```
         <button
          className={`button button-primary button-secondary-${
            isActive ? "active" : "inactive"
          }`}
          onClick={() => setIsActive(!isActive)}
        >
          {isActive ? "Pause" : "Start"}
        </button>
```
Next let's add a reset function to reset the timer.
```
  const reset = () => {
    setSeconds(0);
    setMinutes(0);
    setIsActive(false);
  };
```
  now let's add this function to an onClick for the reset button.

    `  <button className="button btn-danger" onClick={reset}>Reset</button>`

Next, we'll need the timer to actually work. and for that we're going to use the `setInterval` method.
before we do that we're going to need another state to save the current time of the timer since we have both minutes and seconds in two seperate states.

 ` const [currentTime, setTime] = useState(0);`

we're going to use the `useEffect` React Hook to detect whenever `isActive` is true to start the timer inside that function.
```
  useEffect(() => {
    let interval = null;
    if (isActive) {
      const startTime = Date.now() - currentTime;
      interval = setInterval(() => {
        setTime(Date.now() - startTime);
        setSeconds(("0" + (Math.floor(currentTime / 1000) % 60)).slice(-2));
        setMinutes(("0" + (Math.floor(currentTime / 60000) % 60)).slice(-2));
      }, 1000);
    } else if (!isActive && seconds !== 0) {
      clearInterval(interval);
    }
    return () => clearInterval(interval);
  }, [isActive, seconds, minutes]);
```

so basically we first start off by creating a new variable `interval` and setting it to null. After that we 'detect' is `isActive` is true, if yes then we assign the previously cerated variable to a new one that triggers every 1000 milliseconds. If it's false then we clear our the interval and returning `clearInterval`. This is just like calling componentWillUnmount.

and that's it! now you have a perfectly functioning timer.
you could stop here but to make this more fun we can add two new functions to alert the user if the timer is done based on the total time of the brewing method!


this should be your final component.
```
import React, { useState, useEffect } from "react";
//Styling
import "../../timer.css";
import "../../style.css";

const Timer = ({ brewingMethod }) => {
  const [seconds, setSeconds] = useState(0);
  const [minutes, setMinutes] = useState(0);
  const [currentTime, setTime] = useState(0);

  const [isActive, setIsActive] = useState(false);

  const propSeconds = brewingMethod.total_time.substring(
    brewingMethod.total_time.indexOf(":") + 1
  );
  const propMinutes = brewingMethod.total_time.substr(
    0,
    brewingMethod.total_time.indexOf(":")
  );

  const reset = () => {
    setSeconds(0);
    setMinutes(0);
    setIsActive(false);
  };

  const checkTime = () => {
    if (propMinutes === minutes && propSeconds === seconds) {
      alert("all done!");
      setIsActive(!isActive);
    }
  };

  useEffect(() => {
    let interval = null;
    if (isActive) {
      checkTime();
      const startTime = Date.now() - currentTime;
      interval = setInterval(() => {
        setTime(Date.now() - startTime);
        setSeconds(("0" + (Math.floor(currentTime / 1000) % 60)).slice(-2));
        setMinutes(("0" + (Math.floor(currentTime / 60000) % 60)).slice(-2));
      }, 1000);
    } else if (!isActive && seconds !== 0) {
      clearInterval(interval);
    }
    return () => clearInterval(interval);
  }, [isActive, seconds, minutes]);

  return (
    <div className="app">
      <div className="time">
        {minutes}mins:{seconds}s
      </div>
      <div className="row">
        <button
          className={`button button-primary button-secondary-${
            isActive ? "active" : "inactive"
          }`}
          onClick={() => setIsActive(!isActive)}
        >
          {isActive ? "Pause" : "Start"}
        </button>
        <button className="button btn-danger" onClick={reset}>
          Reset
        </button>
      </div>
    </div>
  );
};

export default Timer;
```
