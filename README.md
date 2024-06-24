// Unix timestamp in milliseconds
const timestamp = 1700219463250;

// Create a new Date object
const date = new Date(timestamp);

// Options for date formatting
const options = {
  year: 'numeric',
  month: 'short',
  day: '2-digit',
  hour: '2-digit',
  minute: '2-digit',
  hour12: true
};

// Format the date
const formattedDate = date.toLocaleString('en-US', options);

console.log(formattedDate); // Output: "24 Jun 2024, 11:29 AM"
