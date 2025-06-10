```
import {
  Document,
  Font,
  Image,
  Page,
  StyleSheet,
  Text,
  View,
} from "@react-pdf/renderer";

import outfitBold from "./assets/fonts/Outfit-Bold.ttf";
import outfitRegular from "./assets/fonts/Outfit-Regular.ttf";
import logo from "./assets/logo.svg";

Font.register({
  family: "outfitBold",
  src: outfitBold,
});

Font.register({
  family: "outfitRegular",
  src: outfitRegular,
});

// Create styles
const styles = StyleSheet.create({
  page: {
    flexDirection: "column",
    padding: 20,
    fontFamily: "outfitRegular",
  },
  section: {
    marginBottom: 20,
  },
  heading: {
    fontWeight: "bold",
    fontSize: 22,
    fontFamily: "outfitBold",
  },
  subHeading: {
    color: "#364153",
    fontSize: 10,
    fontWeight: "semibold",
    marginBottom: 8,
    textAlign: "left",
  },
  groupHeading: {
    color: "#101828",
    fontSize: 12,
    fontWeight: "bold",
    marginVertical: 8,
    textAlign: "left",
    fontFamily: "outfitBold",
  },
  paragraph: {
    color: "#101828",
    fontSize: 10,
    lineHeight: 1.5,
    marginVertical: 6,
    fontFamily: "outfitRegular",
  },
  image: {
    width: 100,
    paddingBottom: 10,
  },
  alignRight: {
    textAlign: "right",
  },
  boldText: {
    fontWeight: "bold",
  },
  italicText: {
    fontStyle: "italic",
  },
  underlineText: {
    textDecoration: "underline",
  },
  listItem: {
    fontSize: 12,
    marginBottom: 4,
  },
  link: {
    fontSize: 12,
    color: "blue",
    textDecoration: "underline",
  },
  footer: {
    position: "absolute",
    bottom: 20,
    left: 20,
    right: 20,
    fontSize: 10,
    textAlign: "center",
  },
  table: {
    display: "flex",
    flexDirection: "column",
    width: "100%",
    border: "1px solid #f3f4f6",
    borderBottom: "0px solid #f3f4f6",
  },
  row: {
    flexDirection: "row",
    borderBottom: "1px solid #f3f4f6",
  },
  headerRow: {
    flexDirection: "row",
    backgroundColor: "#f3f4f6",
  },
  cell: {
    flex: 1,
    padding: 4,
    fontSize: 10,
    borderRight: "1px solid #f3f4f6",
  },
  lastCell: {
    borderRight: "none",
  },
  headerText: {
    fontWeight: "bold",
    textAlign: "left",
  },
  pageNumber: {
    position: "absolute",
    fontSize: 8,
    bottom: 30,
    left: 0,
    right: 0,
    textAlign: "center",
    color: "grey",
  },
});

/**
 * Evaluate if a component should be visible based on conditional logic.
 * @param {Object} component - Form component to evaluate
 * @param {Object} valuesMap - Key-value map of form data
 * @returns {boolean} Whether the component should be visible
 */
const isComponentVisible = (component, valuesMap) => {
  const cond = component.conditional;
  if (!cond) return true;

  const actual = valuesMap[cond.when];
  if (cond.show === true) return actual === cond.eq;
  if (cond.show === false) return actual !== cond.eq;

  return true;
};

/**
 * Process components recursively, handling nested structures and conditional logic.
 * @param {Array} components - Array of form components
 * @param {Object} valuesMap - Key-value map of form data
 * @param {Object} formData - Original form data
 * @param {string} parentTitle - Parent component title
 * @param {boolean} parentHidden - Whether parent component is hidden
 * @returns {Array} Processed components with display values
 */
const processComponents = (
  components,
  valuesMap,
  formData,
  parentTitle = null,
  parentHidden = false
) => {
  const result = [];

  for (const component of components) {
    const isVisible = parentHidden
      ? false
      : isComponentVisible(component, valuesMap);
    const currentTitle = component.title || parentTitle;

    if (
      !isVisible &&
      (component.type === "columns" ||
        component.type === "fieldset" ||
        component.type === "panel")
    ) {
      continue; // Skip entire container if hidden
    }

    if (component.components) {
      // Handle nested components (e.g., within panels or fieldsets)
      const nested = processComponents(
        component.components,
        valuesMap,
        formData,
        currentTitle,
        !isVisible
      );
      result.push(...nested);
    } else if (component.columns) {
      // Handle column components
      for (const col of component.columns) {
        const colComponents = processComponents(
          col.components || [],
          valuesMap,
          formData,
          currentTitle,
          !isVisible
        );
        result.push(...colComponents);
      }
    } else if (component.key && component.type !== "htmlelement" && isVisible) {
      result.push({
        label: component.label,
        displayValue: getDisplayValue(component, formData),
        value: formData[component.key],
        type: component.type,
        key: component.key,
        conditional: component.conditional,
        title: currentTitle, // Store the title for grouping
      });
    }
  }

  return result;
};

const getCustomList = (customFunction, formData) => {
  const data = formData;
  console.log("data", data);
  let values;
  eval(customFunction);
  return values;
};

/**
 * Get the display value for a component, handles various input types.
 * @param {Object} component - Form component
 * @param {Object} formData - Form data object
 * @returns {string} Formatted display value
 */
const getDisplayValue = (component, formData) => {
  const value = formData[component.key];
  if (value === undefined || value === null) return "";

  if (component.type === "radio") {
    return component.values?.find((v) => v.value === value)?.label || value;
  }

  if (component.type === "select" && component.widget === "choicesjs") {
    if (component.dataSrc === "url") {
      return formData[component.key];
    }
    if (component.dataSrc === "custom") {
      const options = getCustomList(component?.data?.custom, formData);
      return (
        options?.find((v) => v.value === formData[component.key])?.label ||
        formData[component.key]
      );
    }
    const options = component.data?.values || component.values;
    if (component?.multiple) {
      const valueToLabelMap = options.reduce((map, item) => {
        map[item.value] = item.label;
        return map;
      }, {});
      const res = formData[component.key]
        ?.map((value) => valueToLabelMap[value])
        .filter(Boolean);

      return res?.join(", ");
    } else {
      return (
        options?.find((v) => v.value === formData[component.key])?.label ||
        formData[component.key]
      );
    }
  }

  if (component.type === "selectboxes") {
    return (
      component.values
        ?.filter((v) => formData?.[component.key]?.[v.value])
        .map((opt) => opt.label)
        .join(", ") || value
    );
  }

  if (component.type === "datagrid" && Array.isArray(value)) {
    return value
      .map((item, index) => `Entry ${index + 1}: ${JSON.stringify(item)}`)
      .join("; ");
  }

  return String(value);
};

/**
 * Group components by their section titles and apply conditional logic.
 * @param {Object} schema - Form schema object
 * @param {Object} formData - Form data object
 * @returns {Array} Grouped and filtered form sections
 */
const groupComponentsByTitle = (schema, formData) => {
  const grouped = {};
  const valuesMap = {};

  // First pass: collect all field values for conditional checks
  const allComponents = processComponents(schema.components, {}, formData);
  for (const component of allComponents) {
    if (component.key) {
      valuesMap[component.key] = component.value;
    }
  }

  // Second pass: process components with conditional logic
  const processed = processComponents(schema.components, valuesMap, formData);

  // Group by title
  for (const component of processed) {
    const title = component.title || "Other"; // Use component's assigned title
    if (!grouped[title]) grouped[title] = [];
    grouped[title].push({
      label: component.label,
      displayValue: component.displayValue,
      value: component.value,
      type: component.type,
      key: component.key,
      conditional: component.conditional,
    });
  }

  return Object.entries(grouped).map(([title, data]) => ({ title, data }));
};

function PDFGenerator({ data, ticketId }) {
  const formData = data.formData;
  const bodySchema = data.config?.bodySchema;

  if (!formData || !bodySchema?.components) {
    throw new Error("Invalid JSON structure or missing fields");
  }

  const cleaned = groupComponentsByTitle(bodySchema, formData);

  return (
    <Document>
      <Page size="A4" style={styles.page}>
        <Image style={styles.image} src={logo} />
        <View style={styles.section}>
          <Text style={styles.heading}>Pro Plus</Text>
          <Text style={styles.subHeading}>Ticket Id: {ticketId}</Text>
        </View>

        {/* Render grouped components */}
        {cleaned?.map((collection) => (
          <View style={styles.section} key={collection?.title}>
            <Text style={styles.groupHeading}>{collection?.title}</Text>
            <View style={styles.table}>
              <View style={styles.headerRow}>
                <Text style={[styles.cell, styles.headerText]}>Title</Text>
                <Text style={[styles.cell, styles.headerText, styles.lastCell]}>
                  Value
                </Text>
              </View>
              {collection?.data?.map((item) => (
                <View key={item.key} style={styles.row}>
                  <Text style={styles.cell}>{item?.label || "--"}</Text>
                  <Text style={[styles.cell, styles.lastCell]}>
                    {((typeof item?.displayValue === "string" ||
                      typeof item?.displayValue === "number") &&
                      (item?.displayValue || item?.value)) ||
                      "--"}
                  </Text>
                </View>
              ))}
            </View>
          </View>
        ))}

        <View style={styles.footer}>
          <Text
            style={styles.pageNumber}
            render={({ pageNumber, totalPages }) =>
              `${pageNumber} / ${totalPages}`
            }
            fixed
          />
          <Text style={styles.paragraph}>Report generated by ProPlus</Text>
        </View>
      </Page>
    </Document>
  );
}

export default PDFGenerator;

```
