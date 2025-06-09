const fs = require("fs").promises;

/**
 * Build a key-value map from flat form data to resolve conditional dependencies.
 */
const extractFieldValues = (formSections) => {
  const values = {};
  for (const { data } of formSections) {
    for (const field of data) {
      if (field?.key && field.value !== undefined) {
        values[field.key] = field.value;
      }
    }
  }
  return values;
};

/**
 * Evaluate if a field passes its conditional logic.
 */
const isFieldVisible = (field, valuesMap) => {
  const cond = field.conditional;
  if (!cond) return true;

  const actual = valuesMap[cond.when];

  if (cond.show === true) return actual === cond.eq;
  if (cond.show === false) return actual !== cond.eq;

  return true;
};

/**
 * Removes fields from form sections based on failed conditional logic.
 */
const cleanConditionalFields = (formSections) => {
  const valuesMap = extractFieldValues(formSections);

  return formSections.map(({ title, data }) => ({
    title,
    data: data.filter((field) => isFieldVisible(field, valuesMap)),
  }));
};

/**
 * Get the value to display for a component, handles radios and basic values.
 */
const getDisplayValue = (component, formData) => {
  if (component.type === "radio") {
    return (
      component.values?.find((v) => v.value === formData[component.key])
        ?.label || formData[component.key]
    );
  }
  return formData[component.key];
};

/**
 * Flatten schema into titled sections with form data merged.
 */
const groupComponentsByTitle = (schema, formData) => {
  const grouped = {};

  const traverse = (components, parentTitle = "General") => {
    for (const component of components) {
      const title = component.title || parentTitle;

      if (component.components) {
        traverse(component.components, title);
      } else if (component.columns) {
        for (const col of component.columns) {
          traverse(col.components || [], title);
        }
      } else if (component.key && component.type !== "htmlelement") {
        if (!grouped[title]) grouped[title] = [];
        grouped[title].push({
          label: component.label,
          displayValue: getDisplayValue(component, formData),
          value: formData[component.key],
          type: component.type,
          key: component.key,
          conditional: component.conditional,
        });
      }
    }
  };

  traverse(schema.components);

  return Object.entries(grouped).map(([title, data]) => ({ title, data }));
};

/**
 * Entry point to read, process, and write cleaned form field data.
 */
const processFormFields = async () => {
  try {
    const raw = await fs.readFile("output.json", "utf8");
    if (!raw) throw new Error("File is empty");

    const parsed = JSON.parse(raw);
    const formData = parsed.formData;
    const bodySchema = JSON.parse(parsed.config?.bodySchema || "{}");

    if (!formData || !bodySchema?.components) {
      throw new Error("Invalid JSON structure or missing fields");
    }

    const grouped = groupComponentsByTitle(bodySchema, formData);
    const cleaned = cleanConditionalFields(grouped);

    await fs.writeFile("formFields.json", JSON.stringify(cleaned, null, 2));
    console.log("✅ Cleaned form fields written to formFields.json");
  } catch (err) {
    console.error("❌ Error:", err.message);
    process.exit(1);
  }
};

// Execute script
processFormFields();
