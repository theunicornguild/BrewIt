to do that, the most important thing to do is 'import' the props we sent earlier.

`const Timer = ({ brewingMethod }) => {..}`

then create two new variables one for the minutes and one for the seconds.
so we can split the time that's given in our `data.js` file.

```
  const propSeconds = brewingMethod.total_time.substring(
    brewingMethod.total_time.indexOf(":") + 1
  );
  const propMinutes = brewingMethod.total_time.substr(
    0,
    brewingMethod.total_time.indexOf(":")
  );
```

 we'll then create a function to check whether the time is done or not and pause the timer.

```
const checkTime = () => {
  if (propMinutes === minutes && propSeconds === seconds) {
     alert("all done!");
  setIsActive(!isActive);
  }
};
```
and lastly we'll call that function in `useEffect` in the main if statement to check the timer.
so your final code for `Timer/index.js` should look like this.

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