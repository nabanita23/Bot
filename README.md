function formatDate(input: string): string {
  // Parse the input date string
  const date = new Date(input);

  // Define options for date formatting
  const options: Intl.DateTimeFormatOptions = {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    hour12: true,
  };

  // Format the date parts
  const formattedParts = new Intl.DateTimeFormat('en-GB', options).formatToParts(date);

  // Extract parts
  let day, month, year, hour, minute, dayPeriod;
  formattedParts.forEach(({ type, value }) => {
    switch (type) {
      case 'day':
        day = value;
        break;
      case 'month':
        month = value;
        break;
      case 'year':
        year = value;
        break;
      case 'hour':
        hour = value;
        break;
      case 'minute':
        minute = value;
        break;
      case 'dayPeriod':
        dayPeriod = value;
        break;
    }
  });

  // Construct the formatted date string
  const formattedDate = `${day} ${month} ${year}, ${hour}:${minute} ${dayPeriod}`;

  return formattedDate;
}

// Example usage
const inputDate = "2024-04-10T16:36:37.521+0000";
const formattedDate = formatDate(inputDate);
console.log(formattedDate); // Output: "10 Apr 2024, 04:36 PM"
