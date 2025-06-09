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
  footer: {
    position: 'absolute',
    bottom: 20,
    left: 20,
    right: 20,
    fontSize: 10,
    textAlign: 'center',
  },
})

// Utility function to check if a string contains HTML tags
const containsHTML = (str) => /<\/?[a-z][\s\S]*>/i.test(str)

// Utility function to handle nested objects and arrays
const formatValue = (value) => {
  if (Array.isArray(value)) {
    // Handle arrays by formatting each element
    return value
      .map((item, index) => {
        if (typeof item === 'object' && item !== null) {
          // Format each object in the array
          return `Item ${index + 1}: ${Object.entries(item)
            .map(([key, val]) => `${key}: ${formatValue(val)}`)
            .join(', ')}`
        }
        return `Item ${index + 1}: ${item ?? 'N/A'}`
      })
      .join('\n');
  } else if (typeof value === 'object' && value !== null) {
    // Handle objects by formatting key-value pairs
    return Object.entries(value)
      .map(([key, val]) => `${key}: ${formatValue(val)}`)
      .join(', ');
  }
  return value ?? 'N/A'; // Return 'N/A' for null or undefined values
};

// Utility function to group components by title
function getLeafComponentsGroupedByTitle(schema) {
  const groupedComponents = {}

  function traverse(components, parentTitle = '--') {
    components.forEach((component) => {
      const title = component.title || parentTitle // Use title if present, otherwise fallback to parent title

      if (component.components && component.components.length > 0) {
        traverse(component.components, title)
      } else if (component.columns && component.columns.length > 0) {
        component.columns.forEach((col) => traverse(col.components || [], title))
      } else {
        if (!groupedComponents[title]) {
          groupedComponents[title] = []
        }
        groupedComponents[title].push(component)
      }
    })
  }

  if (schema.components) {
    traverse(schema.components)
  }

  // Convert the grouped object into an array format
  return Object.keys(groupedComponents).map((title) => ({
    title,
    data: groupedComponents[title],
  }))
}

function PDFGenerator({ data, ticketId }) {
  // Parse the bodySchema from the data
  const bodySchema = data.bodySchema || (data.config && JSON.parse(data.config.bodySchema)) || null

  return (
    <Document>
      <Page size="A4" style={styles.page}>
        <Image style={styles.image} src={logo} />
        <View style={styles.section}>
          <Text style={styles.heading}>Pro Plus</Text>
          <Text style={styles.subHeading}>Ticket Id: {ticketId}</Text>
        </View>

        {/* Render grouped components */}
        {getLeafComponentsGroupedByTitle(bodySchema)?.map((collection) => (
          <View style={styles.section} key={collection?.title}>
            <Text style={styles.groupHeading}>{collection?.title}</Text>
            <View style={styles.table}>
              <View style={styles.headerRow}>
                <Text style={[styles.cell]}>Title</Text>
                <Text style={[styles.cell, styles.lastCell]}>Value</Text>
              </View>
              {collection?.data
                ?.filter((item) => !containsHTML(item.label)) // Exclude labels with HTML tags
                .map((item) => {
                  let value;

                  // Handle special cases like accountController
                  if (item.key === 'accountController') {
                    value = formatValue(data?.formData?.accountController);
                  } else {
                    value = formatValue(data?.formData?.[item.key]);
                  }

                  return (
                    <View key={item.key} style={styles.row}>
                      <Text style={styles.cell}>{item.label || 'N/A'}</Text>
                      <Text style={[styles.cell, styles.lastCell]}>{value}</Text>
                    </View>
                  );
                })}
            </View>
          </View>
        ))}

        <View style={styles.footer}>
          <Text
            style={styles.paragraph}
            render={({ pageNumber, totalPages }) => `${pageNumber} / ${totalPages}`}
            fixed
          />
          <Text style={styles.paragraph}>Report generated by ProPlus</Text>
        </View>
      </Page>
    </Document>
  )
}

export default PDFGenerator
