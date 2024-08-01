fileChange(event) {
  console.log(event, event[event.length - 1]);
  
  // Check if the number of documents exceeds the limit
  if (this.documents.length >= 2) {
    this.createErrorAlert('You can only upload a maximum of 2 documents.');
    return;
  }

  if (event[event.length - 1].size > constants.maxFileSize || event[event.length - 1].size === 0) {
    this.createErrorAlert('File size should be minimum 1 Byte or maximum 25 MB');
  } else {
    if (!this.documentCommentDisable) {
      this.uploadFile(event[event.length - 1]);
    }
  }
}
