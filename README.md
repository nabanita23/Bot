function convertDate(dateStr) {
  // Split the input date string by '/'
  const [day, month, year] = dateStr.split('/');
  
  // Create an array of month names
  const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
  
  // Get the month name corresponding to the month number
  const monthName = monthNames[parseInt(month) - 1];
  
  // Return the date in the desired format
  return `${day}-${monthName}-${year}`;
}
