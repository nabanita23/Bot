```
import React from 'react'
import { Page, Text, View, Document, StyleSheet, Font, Image } from '@react-pdf/renderer'
const logo = require('../../images/logo.jpg')

const outfitBold = require('../../fonts/Outfit-Bold.ttf')
const outfitRegular = require('../../fonts/Outfit-Regular.ttf')

Font.register({
  family: 'outfitBold',
  src: outfitBold,
})

Font.register({
  family: 'outfitRegular',
  src: outfitRegular,
})

// Create styles
const styles = StyleSheet.create({
  page: {
    flexDirection: 'column',
    padding: 20,
    fontFamily: 'outfitRegular',
  },
  section: {
    marginBottom: 20,
  },
  heading: {
    fontWeight: 'bold',
    fontSize: 18,
    fontFamily: 'outfitBold',
  },
  subHeading: {
    color: '#364153',
    fontSize: 10,
    fontWeight: 'semibold',
    marginBottom: 8,
    textAlign: 'left',
  },
  groupHeading: {
    color: '#101828',
    fontSize: 12,
    fontWeight: 'bold',
    marginVertical: 8,
    textAlign: 'left',
  },
  paragraph: {
    color: '#101828',
    fontSize: 10,
    lineHeight: 1.5,
    marginVertical: 6,
    fontFamily: 'outfitRegular',
  },
  image: {
    width: 100,
    paddingBottom: 10,
  },
  alignRight: {
    textAlign: 'right',
  },
  boldText: {
    fontWeight: 'bold',
  },
  italicText: {
    fontStyle: 'italic',
  },
  underlineText: {
    textDecoration: 'underline',
  },
  listItem: {
    fontSize: 12,
    marginBottom: 4,
  },
  link: {
    fontSize: 12,
    color: 'blue',
    textDecoration: 'underline',
  },
  footer: {
    position: 'absolute',
    bottom: 20,
    left: 20,
    right: 20,
    fontSize: 10,
    textAlign: 'center',
  },
  table: {
    display: 'flex',
    flexDirection: 'column',
    width: '100%',
    border: '1px solid #d1d5dc',
  },
  row: {
    flexDirection: 'row',
    borderBottom: '1px solid #d1d5dc',
  },
  headerRow: {
    flexDirection: 'row',
    backgroundColor: '#f3f4f6',
    borderTop: '1px solid #d1d5dc',
    borderBottom: '1px solid #d1d5dc',
  },
  cell: {
    flex: 1,
    padding: 4,
    fontSize: 10,
    borderRight: '1px solid #d1d5dc',
  },
  lastCell: {
    borderRight: 'none',
  },
  headerText: {
    fontWeight: 'bold',
    textAlign: 'left',
  },
  pageNumber: {
    position: 'absolute',
    fontSize: 8,
    bottom: 30,
    left: 0,
    right: 0,
    textAlign: 'center',
    color: 'grey',
  },
})

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

const getCustomList = (customFunction, formData) => {
  const data = formData;
  console.log('data', data)
  let values;
  eval(customFunction);
  return values
}

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
  if (component.type === "select" && component.widget === 'choicesjs') {
    if (component.dataSrc === 'url') {
      return formData[component.key]
    }
    if (component.dataSrc === 'custom') {
      const options = getCustomList(component?.data?.custom, formData);
      return (
        options?.find((v) => v.value === formData[component.key])
          ?.label || formData[component.key]
      );
    }
    const options = component.data?.values || component.values;
    if (component?.multiple) {
      const valueToLabelMap = options.reduce((map, item) => {
        map[item.value] = item.label;
        return map;
      }, {});
      const res = formData[component.key]?.map(value => valueToLabelMap[value]).filter(Boolean)

      return res?.join(', ');
    } else {
      return (
        options?.find((v) => v.value === formData[component.key])
          ?.label || formData[component.key]
      );
    }
  }
  if (component.type === "selectboxes") {
    const filtered = component.values?.filter((v) =>  formData?.[component.key]?.[v.value])

    return filtered.map(option => option.label)?.join(', ') || formData[component.key];
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

function PDFGenerator({ data, ticketId }) {

  const formData = data.formData;
  const bodySchema = JSON.parse(data.config?.bodySchema || "{}");

  if (!formData || !bodySchema?.components) {
    throw new Error("Invalid JSON structure or missing fields");
  }

  const grouped = groupComponentsByTitle(bodySchema, formData);
  const cleaned = cleanConditionalFields(grouped);

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
                <Text style={[styles.cell, styles.headerText, styles.lastCell]}>Value</Text>
              </View>
              {collection?.data?.map((item) => (
                <View key={item.key} style={styles.row}>
                  <Text style={styles.cell}>{item?.label || '--'}</Text>
                  <Text style={[styles.cell, styles.lastCell]}>
                    {(typeof item?.displayValue === 'string' || typeof item?.displayValue === 'number') && (item?.displayValue || item?.value) || '--'}
                  </Text>
                </View>
              ))}
            </View>
          </View>
        ))}

        <View style={styles.footer}>
          <Text
            style={styles.pageNumber}
            render={({ pageNumber, totalPages }) => `${pageNumber} / ${totalPages}`}
            fixed
          />
          <Text style={styles.paragraph}>Report generated by ProPlus</Text>
        </View>
      </Page>
    </Document>
  );
}

export default PDFGenerator

```
