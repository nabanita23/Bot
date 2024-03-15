----
import React, { useState } from 'react';

// Define a type for the state variable
type CountState = number;

function Counter() {
  // Declare a state variable named "count" initialized to 0
  const [count, setCount] = useState<CountState>(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      {/* Button to increment the count */}
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default Counter;

example
