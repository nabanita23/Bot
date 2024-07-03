const datePattern = /^\d{2}\/\d{2}\/\d{4}$/;

function isValidDateFormat(dateString) {
  return datePattern.test(dateString);
}

let dateString1 = "24/04/2024";
let dateString2 = "2024/04/24";

console.log(isValidDateFormat(dateString1)); // Output: true
console.log(isValidDateFormat(dateString2)); // Output: false
pppp

function convertToDate(dateString) {
  // Split the date string into an array
  let dateParts = dateString.split('/');

  // Rearrange the array elements to match the Date constructor format (YYYY, MM, DD)
  // Note: Months in JavaScript Date object are 0-indexed, so subtract 1 from the month
  let day = parseInt(dateParts[0], 10);
  let month = parseInt(dateParts[1], 10) - 1;
  let year = parseInt(dateParts[2], 10);

  // Create a new Date object
  let date = new Date(year, month, day);

  return date;
}

let dateString = "24/04/2024";
let date = convertToDate(dateString);
console.log(date); // Output: Wed Apr 24 2024 00:00:00 GMT+0000 (Coordinated Universal Time)
