import React from 'react';
import ReactDOM from 'react-dom';
import FormWidget from './FormWidget';

const App = () => {
  const handleSuccess = (result) => {
    console.log('Form submitted successfully:', result);
  };

  const handleError = (error) => {
    console.error('Error submitting form:', error);
  };

  return (
    <div>
      <h1>Embed Form Widget</h1>
      <FormWidget
        apiUrl="https://example.com/api/submit"
        fields={[
          { name: 'name', label: 'Name', required: true },
          { name: 'email', label: 'Email', type: 'email', required: true },
          { name: 'message', label: 'Message', type: 'textarea' },
        ]}
        onSuccess={handleSuccess}
        onError={handleError}
      />
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById('root'));
