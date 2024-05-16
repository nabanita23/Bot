import React, { useState, useEffect } from 'react';

const App = () => {
  const [options1, setOptions1] = useState([]);
  const [options2, setOptions2] = useState([]);
  const [options3, setOptions3] = useState([]);
  const [selectedOption1, setSelectedOption1] = useState('');
  const [selectedOption2, setSelectedOption2] = useState('');
  const [selectedOption3, setSelectedOption3] = useState('');

  // Mock data for initial load
  const mockData1 = [{ id: 1, name: 'Option 1' }, { id: 2, name: 'Option 2' }];
  const mockData2 = [{ id: 1, name: 'Option A' }, { id: 2, name: 'Option B' }];
  const mockData3 = [{ id: 1, name: 'Option X' }, { id: 2, name: 'Option Y' }];

  useEffect(() => {
    // Fetch data for dropdown 1 from API
    // Replace 'fetchApi1' with your actual API call
    fetchApi1().then(data => {
      // Update dropdown options
      setOptions1(data);
    }).catch(error => {
      // Handle error
      console.error('Error fetching data for dropdown 1:', error);
    });

    // Fetch data for dropdown 2 from API
    // Replace 'fetchApi2' with your actual API call
    fetchApi2().then(data => {
      // Update dropdown options
      setOptions2(data);
    }).catch(error => {
      // Handle error
      console.error('Error fetching data for dropdown 2:', error);
    });

    // Fetch data for dropdown 3 from API
    // Replace 'fetchApi3' with your actual API call
    fetchApi3().then(data => {
      // Update dropdown options
      setOptions3(data);
    }).catch(error => {
      // Handle error
      console.error('Error fetching data for dropdown 3:', error);
    });
  }, []);

  const handleDropdown1Change = (event) => {
    const value = event.target.value;
    setSelectedOption1(value);

    // Trigger API call for dropdown 2 based on selection in dropdown 1
    // Replace 'fetchApiForDropdown2' with your actual API call
    fetchApiForDropdown2(value).then(data => {
      // Update dropdown options
      setOptions2(data);
      setSelectedOption2('');
    }).catch(error => {
      // Handle error
      console.error('Error fetching data for dropdown 2 based on selection:', error);
    });
  };

  const handleDropdown2Change = (event) => {
    const value = event.target.value;
    setSelectedOption2(value);

    // Trigger API call for dropdown 3 based on selection in dropdown 2
    // Replace 'fetchApiForDropdown3' with your actual API call
    fetchApiForDropdown3(value).then(data => {
      // Update dropdown options
      setOptions3(data);
      setSelectedOption3('');
    }).catch(error => {
      // Handle error
      console.error('Error fetching data for dropdown 3 based on selection:', error);
    });
  };

  const handleDropdown3Change = (event) => {
    const value = event.target.value;
    setSelectedOption3(value);
  };

  return (
    <div>
      <select value={selectedOption1} onChange={handleDropdown1Change}>
        {options1.map(option => (
          <option key={option.id} value={option.id}>{option.name}</option>
        ))}
      </select>
      <select value={selectedOption2} onChange={handleDropdown2Change}>
        {options2.map(option => (
          <option key={option.id} value={option.id}>{option.name}</option>
        ))}
      </select>
      <select value={selectedOption3} onChange={handleDropdown3Change}>
        {options3.map(option => (
          <option key={option.id} value={option.id}>{option.name}</option>
        ))}
      </select>
    </div>
  );
};

export default App;
