function trimNonASCIICharacters(str) {
  return str.replace(/[^\x00-\x7F]/g, '');
}

// Example usage:
const originalString = "Héllö wörld! Thïs has non-ASCII charàctérs.";
const trimmedString = trimNonASCIICharacters(originalString);
console.log(trimmedString); // Output: "Hll wrld! Ths has non-ASCII charctrs."
