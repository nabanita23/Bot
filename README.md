function formatKey(key) {
  return key.replace(/([A-Z])/g, ' $1') // Add space before uppercase letters
            .replace(/^./, str => str.toUpperCase()); // Capitalize the first letter
}

function flattenObjectToArray(obj, result = []) {
  for (const key in obj) {
    if (Object.prototype.hasOwnProperty.call(obj, key)) {
      if (typeof obj[key] === 'object' && obj[key] !== null && !Array.isArray(obj[key])) {
        flattenObjectToArray(obj[key], result);
      } else {
        result.push({ title: formatKey(key), value: obj[key] });
      }
    }
  }
  return result;
}

// Example usage
const nestedObj = {
  user: {
    firstName: 'John',
    lastName: 'Doe',
    address: {
      cityName: 'New York',
      zipCode: '10001',
    },
    contactDetails: {
      emailAddress: 'john@example.com',
      phoneNumber: '123456789',
    },
  },
};

console.log(flattenObjectToArray(nestedObj));
