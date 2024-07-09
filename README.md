function epochToFormattedDate(epoch) {
    const date = new Date(epoch * 1000); // Convert epoch to milliseconds

    const daysOfWeek = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
    const monthsOfYear = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

    const day = daysOfWeek[date.getUTCDay()];
    const month = monthsOfYear[date.getUTCMonth()];
    const dayOfMonth = date.getUTCDate().toString().padStart(2, '0');
    const year = date.getUTCFullYear();
    const hours = date.getUTCHours().toString().padStart(2, '0');
    const minutes = date.getUTCMinutes().toString().padStart(2, '0');
    const seconds = date.getUTCSeconds().toString().padStart(2, '0');

    // Format the date string
    const formattedDate = `${day} ${month} ${dayOfMonth} ${hours}:${minutes}:${seconds} CET ${year}`;
    
    return formattedDate;
}

const epoch = 1717611005; // Example epoch timestamp
console.log(epochToFormattedDate(epoch)); // Outputs: Wed Jun 05 16:10:05 CET 2024
