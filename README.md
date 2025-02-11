function generateBreadcrumbs(obj, keys) {
    return keys
        .filter(key => obj.hasOwnProperty(key)) // Ensure the key exists in the object
        .map(key => obj[key])
        .join(" > "); // Join breadcrumb items with a separator
}

// Example object
const pageData = {
    home: "Home",
    category: "Technology",
    subcategory: "AI",
    article: "Smart Code Review"
};

// Specify the keys to be included in breadcrumbs
const breadcrumbKeys = ["home", "category", "subcategory", "article"];

const breadcrumbs = generateBreadcrumbs(pageData, breadcrumbKeys);
console.log(breadcrumbs); // Output: Home > Technology > AI > Smart Code Review
