Wed Jun 05 16:10:05 IST 2024


const dateFormat = require('dateformat');

// Given timestamp
let timestamp = "Wed Jun 05 16:10:05 IST 2024";

// Manually parse the timestamp and remove the time zone abbreviation
let cleanTimestamp = timestamp.replace('IST', '');

// Create a Date object from the cleaned timestamp
let date = new Date(cleanTimestamp + ' GMT+0530'); // Assuming IST is GMT+0530

// Format the date using dateformat
let formattedDate = dateFormat(date, "dd mmm yyyy hh:MM TT");

console.log(formattedDate); // Output: 05 Jun 2024 04:10 PM

