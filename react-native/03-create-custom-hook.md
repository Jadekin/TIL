# Creating a custom hook: why and how

Creating a custom hook in React allows you to encapsulate reusable logic that can be shared across different components. Hooks are these functions that let you use React features in functional components and they follow a specific naming convention by prefixing the name with "use" (e.g., useCustomHook).

## Steps
### 1: Create the custom hook function

Start by creating a new JavaScript file (e.g., ``useCustomHook.js``) where you'll define your custom hook function. It should contain the logic you want to reuse and It can use built-in React hooks or other custom hooks as needed.

```javascript
// useCustomHook.js
import { useState, useEffect } from 'react';

function useCustomHook(initialValue) {
  const [value, setValue] = useState(initialValue);

  useEffect(() => {
    // Some side effects or logic you want to perform
    // This may include API calls, event listeners, etc.
    // Remember to clean up any resources in the return function
    return () => {
      // Clean-up code here (if any)
    };
  }, [/* dependencies */]);

  const updateValue = (newValue) => {
    setValue(newValue);
  };

  return {
    value,
    updateValue,
  };
}

export default useCustomHook;
```

### Step 2: Using the custom hook

To use your custom hook in a functional component, import and call it. You can destructure the returned values from the hook to access the state and functions it provides.

```javascript
import React from 'react';
import useCustomHook from './useCustomHook';

function MyComponent() {
  const { value, updateValue } = useCustomHook(0);

  const handleButtonClick = () => {
    updateValue(value + 1);
  };

  return (
    <div>
      <p>Value: {value}</p>
      <button onClick={handleButtonClick}>Increment</button>
    </div>
  );
}

export default MyComponent;
```

## Best practices for using custom hooks:

- Keep hooks focused and reusable: Make sure your custom hooks serve a specific purpose and can be used across different components. This improves maintainability and reusability. E.g. ```useAPI```.

- Follow the "use" prefix convention: Naming your custom hook with the "use" prefix signals to developers that it's a hook and should adhere to the rules of hooks.

- Avoid nesting hooks within functions or conditionals: Hooks should be called at the top level of functional components and not within loops, conditions, or nested functions.

- Limit the number of custom hooks: While custom hooks are powerful, try not to overuse them. Only create a custom hook if you find yourself duplicating the same logic across multiple components.
