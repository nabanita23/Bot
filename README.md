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
