function trimNonASCIICharacters(str) {
  return str.replace(/[^\x00-\x7F]/g, '');
}

// Example usage:
const originalString = "Héllö wörld! Thïs has non-ASCII charàctérs.";
const trimmedString = trimNonASCIICharacters(originalString);
console.log(trimmedString); // Output: "Hll wrld! Ths has non-ASCII charctrs."
/[^a-zA-Z\s\d]|[^\u0000-\u007F\u0080-\u03FF]/g
