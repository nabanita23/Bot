import React from 'react';
import { Document, Page, View, Text } from '@react-pdf/renderer';
import styles from './styles'; // Import the styles

const data = [
  { title: "First Name", value: "John" },
  { title: "Last Name", value: "Doe" },
  { title: "City Name", value: "New York" },
  { title: "Zip Code", value: "10001" },
  { title: "Email Address", value: "john@example.com" },
  { title: "Phone Number", value: "123456789" }
];

const MyPDF = () => (
  <Document>
    <Page size="A4" style={{ padding: 20 }}>
      {/* Table Header */}
      <View style={styles.table}>
        <View style={styles.headerRow}>
          <Text style={[styles.cell, styles.headerText]}>Title</Text>
          <Text style={[styles.cell, styles.headerText, styles.lastCell]}>Value</Text>
        </View>

        {/* Table Rows */}
        {data.map((item, index) => (
          <View key={index} style={styles.row}>
            <Text style={styles.cell}>{item.title}</Text>
            <Text style={[styles.cell, styles.lastCell]}>{item.value}</Text>
          </View>
        ))}
      </View>
    </Page>
  </Document>
);

export default MyPDF;


import { StyleSheet } from '@react-pdf/renderer';

const styles = StyleSheet.create({
  table: {
    display: 'flex',
    flexDirection: 'column',
    width: '100%',
    border: '1px solid #000',
  },
  row: {
    flexDirection: 'row',
    borderBottom: '1px solid #000',
  },
  headerRow: {
    flexDirection: 'row',
    backgroundColor: '#f2f2f2',
    borderBottom: '1px solid #000',
  },
  cell: {
    flex: 1,
    padding: 6,
    fontSize: 12,
    borderRight: '1px solid #000',
  },
  lastCell: {
    borderRight: 'none',
  },
  headerText: {
    fontWeight: 'bold',
    textAlign: 'left',
  },
});

export default styles;

