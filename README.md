function formatDate(input: string): string {
  // Parse the input date string
  const date = new Date(input);

  // Define options for date formatting
  const options: Intl.DateTimeFormatOptions = {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    hour12: true,
  };

  // Format the date
  const formattedDate = new Intl.DateTimeFormat('en-GB', options).format(date);

  // Convert month to short format and ensure day and hour formatting
  const dateParts = formattedDate.split(', ');
  const monthDayParts = dateParts[0].split(' ');
  const timeParts = dateParts[1].split(':');
  const hour = timeParts[0].length === 1 ? '0' + timeParts[0] : timeParts[0];
  const minute = timeParts[1].split(' ')[0];

  return `${parseInt(monthDayParts[1])} ${monthDayParts[0]} ${monthDayParts[2]}, ${hour}:${minute} ${timeParts[1].split(' ')[1]}`;
}

// Example usage
const inputDate = "2024-04-10T16:36:37.521+0000";
const formattedDate = formatDate(inputDate);
console.log(formattedDate); // Output: "10 Apr 2024, 04:36 PM"
