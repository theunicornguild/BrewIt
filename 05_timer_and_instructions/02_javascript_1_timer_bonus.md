to do that, the most important thing to do is 'import' the props we sent earlier.

//Mariam: the code provided in the previous step already has the following additions (may cause confusion lol)
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

lastly we'll create a function to check whether the time is done or not and pause the timer.

```
 const endTimer = () => {
    alert("all done!");
    setIsActive(!isActive);
  };
```

```
const checkTime = () => {
  if (propMinutes === minutes && propSeconds === seconds) {
     alert("all done!");
  setIsActive(!isActive);
  }
};
```
