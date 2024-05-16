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
