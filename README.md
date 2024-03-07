import React, { useState } from 'react';

const DynamicIframeComponent = () => {
  // State variables to store dynamic parameters
  const [param1, setParam1] = useState('defaultParam1');
  const [param2, setParam2] = useState('defaultParam2');

  // Function to update parameters
  const updateParams = () => {
    // Update parameters as needed
    setParam1('newParam1');
    setParam2('newParam2');
  };

  return (
    <div>
      {/* Button to trigger parameter update */}
      <button onClick={updateParams}>Update Parameters</button>

      {/* Iframe with dynamic parameters */}
      <iframe
        title="DynamicIframe"
        width="600"
        height="400"
        src={`https://example.com?param1=${param1}&param2=${param2}`}
        frameBorder="0"
        allowFullScreen
      />
    </div>
  );
};

export default DynamicIframeComponent;
