<div id="widget-container"></div>
<script>
  new EmbeddableFormWidget({
    apiUrl: 'https://api.example.com/data',
    formFields: [
      { name: 'name', label: 'Name', type: 'text' },
      { name: 'email', label: 'Email', type: 'email' },
    ],
    onSubmit: (data) => console.log('Form submitted:', data),
  }).render(document.getElementById('widget-container'));
</script>
