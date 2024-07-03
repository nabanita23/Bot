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
