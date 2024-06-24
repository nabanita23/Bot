// Unix timestamp in milliseconds
const timestamp = 1700219463250;

// Create a new Date object
const date = new Date(timestamp);

// Options for date formatting with explicit type
const options: Intl.DateTimeFormatOptions = {
  year: 'numeric',
  month: 'short',
  day: '2-digit',
  hour: '2-digit',
  minute: '2-digit',
  hour12: true
};

// Format the date for Swiss locale and remove dots
const formattedDateParts = date.toLocaleDateString('de-CH', options).replace(/\./g, '');
const time = date.toLocaleTimeString('de-CH', options).replace(/\./g, '');

// Combine the date and time parts
const formattedDate = `${formattedDateParts}, ${time}`;

console.log(formattedDate); // Output: "24 Jun 2024, 11:29 vorm."
