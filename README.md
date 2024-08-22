function compareStringsIgnoreCamelCase(str1, str2) {
    const normalizeString = (str) => {
        return str
            .replace(/([a-z])([A-Z])/g, '$1 $2') // Add space before uppercase letters
            .toLowerCase()                      // Convert to lowercase
            .replace(/\s+/g, '');               // Remove spaces
    };

    return normalizeString(str1) === normalizeString(str2);
}

// Examples
console.log(compareStringsIgnoreCamelCase('myVariableName', 'myvariablename')); // true
console.log(compareStringsIgnoreCamelCase('anotherExampleHere', 'anotherexamplehere')); // true
console.log(compareStringsIgnoreCamelCase('TestStringOne', 'teststringone')); // true
