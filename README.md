

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

