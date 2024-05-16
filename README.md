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
