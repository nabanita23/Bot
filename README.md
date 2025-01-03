import React, { useState, useEffect } from 'react';

const EmbeddableFormWidget = ({ apiUrl, formFields, onSubmit }) => {
  const [formData, setFormData] = useState({});
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    if (apiUrl) {
      setLoading(true);
      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          setFormData(data);
          setLoading(false);
        })
        .catch((error) => {
          console.error('Error fetching data:', error);
          setLoading(false);
        });
    }
  }, [apiUrl]);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (onSubmit) onSubmit(formData);
  };

  if (loading) return <div>Loading...</div>;

  return (
    <form onSubmit={handleSubmit}>
      {formFields.map((field) => (
        <div key={field.name}>
          <label htmlFor={field.name}>{field.label}</label>
          <input
            type={field.type}
            id={field.name}
            name={field.name}
            value={formData[field.name] || ''}
            onChange={handleChange}
          />
        </div>
      ))}
      <button type="submit">Submit</button>
    </form>
  );
};

export default EmbeddableFormWidget;
