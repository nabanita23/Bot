import React, { useState, useEffect } from 'react';
import axios from 'axios';

function CascadingDropdown() {
    const [options1, setOptions1] = useState([]);
    const [selectedOption1, setSelectedOption1] = useState('');
    const [options2, setOptions2] = useState([]);
    const [selectedOption2, setSelectedOption2] = useState('');
    const [options3, setOptions3] = useState([]);
    const [selectedOption3, setSelectedOption3] = useState('');

    useEffect(() => {
        // Fetch data for the first dropdown
        axios.get('api/endpoint1')
            .then(response => {
                setOptions1(response.data);
            })
            .catch(error => {
                console.error('Error fetching data for dropdown 1:', error);
            });
    }, []);

    useEffect(() => {
        if (selectedOption1 !== '') {
            // Fetch data for the second dropdown based on the selected value of the first dropdown
            axios.get(`api/endpoint2?param=${selectedOption1}`)
                .then(response => {
                    setOptions2(response.data);
                })
                .catch(error => {
                    console.error('Error fetching data for dropdown 2:', error);
                });
        }
    }, [selectedOption1]);

    useEffect(() => {
        if (selectedOption2 !== '') {
            // Fetch data for the third dropdown based on the selected value of the second dropdown
            axios.get(`api/endpoint3?param=${selectedOption2}`)
                .then(response => {
                    setOptions3(response.data);
                })
                .catch(error => {
                    console.error('Error fetching data for dropdown 3:', error);
                });
        }
    }, [selectedOption2]);

    const handleOption1Change = (event) => {
        setSelectedOption1(event.target.value);
        setSelectedOption2(''); // Reset second dropdown when the first dropdown changes
        setSelectedOption3(''); // Reset third dropdown when the first dropdown changes
    };

    const handleOption2Change = (event) => {
        setSelectedOption2(event.target.value);
        setSelectedOption3(''); // Reset third dropdown when the second dropdown changes
    };

    const handleOption3Change = (event) => {
        setSelectedOption3(event.target.value);
    };

    return (
        <div>
            <select value={selectedOption1} onChange={handleOption1Change}>
                <option value="">Select Option 1</option>
                {options1.map(option => (
                    <option key={option.id} value={option.value}>{option.label}</option>
                ))}
            </select>
            <select value={selectedOption2} onChange={handleOption2Change}>
                <option value="">Select Option 2</option>
                {options2.map(option => (
                    <option key={option.id} value={option.value}>{option.label}</option>
                ))}
            </select>
            <select value={selectedOption3} onChange={handleOption3Change}>
                <option value="">Select Option 3</option>
                {options3.map(option => (
                    <option key={option.id} value={option.value}>{option.label}</option>
                ))}
            </select>
        </div>
    );
}

export default CascadingDropdown;
-------------------------------------------------------------------------------------------------------------

// mockData.js
export const countries = [
  { id: 1, name: "USA" },
  { id: 2, name: "Canada" },
  // Other countries...
];

export const states = [
  { id: 1, name: "California", countryId: 1 },
  { id: 2, name: "New York", countryId: 1 },
  { id: 3, name: "Ontario", countryId: 2 },
  // Other states...
];

export const cities = [
  { id: 1, name: "Los Angeles", stateId: 1 },
  { id: 2, name: "San Francisco", stateId: 1 },
  { id: 3, name: "New York City", stateId: 2 },
  // Other cities...
];
-------------------------------------------------------


// MainComponent.js
import React, { useState } from "react";
import Dropdown from "./Dropdown";
import { countries, states, cities } from "./mockData";

const MainComponent = () => {
  const [selectedCountry, setSelectedCountry] = useState("");
  const [selectedState, setSelectedState] = useState("");
  const [selectedCity, setSelectedCity] = useState("");

  const handleCountryChange = e => {
    setSelectedCountry(e.target.value);
    setSelectedState(""); // Reset state when country changes
    setSelectedCity(""); // Reset city when country changes
  };

  const handleStateChange = e => {
    setSelectedState(e.target.value);
    setSelectedCity(""); // Reset city when state changes
  };

  const handleCityChange = e => {
    setSelectedCity(e.target.value);
  };

  return (
    <div>
      <h1>Cascading Dropdown Example</h1>
      <Dropdown
        label="Country"
        options={countries}
        value={selectedCountry}
        onChange={handleCountryChange}
      />
      {selectedCountry && (
        <Dropdown
          label="State"
          options={states.filter(state => state.countryId === parseInt(selectedCountry))}
          value={selectedState}
          onChange={handleStateChange}
        />
      )}
      {selectedState && (
        <Dropdown
          label="City"
          options={cities.filter(city => city.stateId === parseInt(selectedState))}
          value={selectedCity}
          onChange={handleCityChange}
        />
      )}
      <div>
        Selected Country: {selectedCountry}, Selected State: {selectedState}, Selected City: {selectedCity}
      </div>
    </div>
  );
};

export default MainComponent;
