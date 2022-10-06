---
description: Hooks in react/React-native
---

# Hooks in React

### `This info is taken from w3school.com`

``[`https://www.w3schools.com/react/react_hooks.asp`](https://www.w3schools.com/react/react\_hooks.asp)``

### What is a Hook?

Hooks allow us to "hook" into React features such as state and life-cycle methods.

#### Example:

```tsx
import React, { useState } from "react";
import {View, Text} from 'react-native';

const App = () => {
    
    const [color, setcolor] = useState("blue");
    
    return(
    <View>
  <Text>My favorite color is {color}!</Text>
      <Button
          title="press me"
        onClick={() => setColor("blue")}/>
    </View>
    )
.....
```



### Types of Hooks.

There are approximately 8 Hooks are there in React. Which are listed below..

1. &#x20;[useState](./#usestate-hook)
2. [useEffect](./#useeffect-hook)
3. useContext
4. useRef
5. useReducer
6. useCallback
7. useMemo



### useState Hook:

1. The React `useState` Hook allows us to track state in a function component
2. State generally refers to data or properties that need to be tracking in an application.
3. We initialize our state by calling `useState` in our function component.

```tsx
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("");
}
```

`4. useState` accepts an initial state and returns two values:

* The current state.
* A function that updates the state.

`For more info go to this website`&#x20;

[`https://www.w3schools.com/react/react_usestate.asp`](https://www.w3schools.com/react/react\_usestate.asp)``



### `useEffect Hook:`

1. The `useEffect` Hook allows you to perform side effects in your components.
2. Some examples of side effects are: fetching data, directly updating the DOM, and timers.
3.  `useEffect` accepts two arguments. The second argument is optional.

    `useEffect(<function>, <dependency>)`
4. `For more info go to this website` [`https://www.w3schools.com/react/react_useeffect.asp`](https://www.w3schools.com/react/react\_useeffect.asp)``
