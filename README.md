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
