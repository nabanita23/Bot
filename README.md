// App.js
import React, { useState, useEffect } from 'react';
import DropdownComponent from './DropdownComponent';

const App = () => {
  const [firstOptions, setFirstOptions] = useState([]);
  const [secondOptions, setSecondOptions] = useState([]);
  const [thirdOptions, setThirdOptions] = useState([]);
  const [selectedFirst, setSelectedFirst] = useState('');
  const [selectedSecond, setSelectedSecond] = useState('');
  const [selectedThird, setSelectedThird] = useState('');

  useEffect(() => {
    // Fetch first dropdown data
    fetchFirstOptions();
  }, []);

  const fetchFirstOptions = async () => {
    // Mock API call or actual API call
    const response = await fetch('mock_first_dropdown_data.json');
    const data = await response.json();
    setFirstOptions(data);
  };

  const fetchSecondOptions = async () => {
    // Make API call based on selected value from first dropdown
    // Example: fetch(`/api/second-dropdown?firstValue=${selectedFirst}`)
    const response = await fetch('mock_second_dropdown_data.json');
    const data = await response.json();
    setSecondOptions(data);
  };

  const fetchThirdOptions = async () => {
    // Make API call based on selected value from second dropdown
    // Example: fetch(`/api/third-dropdown?secondValue=${selectedSecond}`)
    const response = await fetch('mock_third_dropdown_data.json');
    const data = await response.json();
    setThirdOptions(data);
  };

  const handleFirstChange = (e) => {
    setSelectedFirst(e.target.value);
    setSelectedSecond('');
    setSelectedThird('');
    fetchSecondOptions();
  };

  const handleSecondChange = (e) => {
    setSelectedSecond(e.target.value);
    setSelectedThird('');
    fetchThirdOptions();
  };

  const handleThirdChange = (e) => {
    setSelectedThird(e.target.value);
  };

  return (
    <div>
      <h1>Cascading Dropdowns</h1>
      <DropdownComponent options={firstOptions} onChange={handleFirstChange} />
      {selectedFirst && (
        <DropdownComponent options={secondOptions} onChange={handleSecondChange} />
      )}
      {selectedSecond && (
        <DropdownComponent options={thirdOptions} onChange={handleThirdChange} />
      )}
    </div>
  );
};

export default App;
