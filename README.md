   const files = event.target.files; // Get the list of files
    if (files.length > 2) {
        this.createErrorAlert('You can only upload a maximum of 2 files.');
        return; // Exit the function if file count exceeds the limit
    }
