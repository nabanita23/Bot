import { StyleSheet } from '@react-pdf/renderer';

const styles = StyleSheet.create({
  page: {
    flexDirection: 'column',
    padding: 20,
    fontFamily: 'Helvetica',
  },
  heading: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
    textAlign: 'center',
  },
  subHeading: {
    fontSize: 14,
    fontWeight: 'semibold',
    marginBottom: 8,
    textAlign: 'left',
  },
  paragraph: {
    fontSize: 12,
    lineHeight: 1.5,
    textAlign: 'justify',
    marginBottom: 6,
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
});

export default styles;
