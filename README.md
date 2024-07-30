fileChange(event) {
    const files = event.target.files; // Get the list of files from the event

    if (files.length > 2) {
        this.createErrorAlert('You can only upload a maximum of 2 files.');
        return; // Exit the function if more than 2 files are selected
    }

    for (let i = 0; i < files.length; i++) {
        const file = files[i];
        if (file.size > constants.maxFileSize || file.size === 0) {
            this.createErrorAlert('File size should be minimum 1 Byte or maximum 25 MB');
            return; // Exit the function if any file fails size validation
        }
    }

    if (!this.documentCommentDisable) {
        for (let i = 0; i < files.length; i++) {
            this.uploadFile(files[i]);
        }
    }
}

uploadFile(file) {
    console.log(file, this.uploadedfile);

    const formData = new FormData();
    const aa = JSON.stringify({
        docMetaData: {
            contentType: 'WM Audit Evidence',
            docName: file.name,
            wmISEncrypted: 'NO',
            wmOpsWorkstationComboID: '00000',
            wmOpsWorkstationID: this.workhubContextTask.activity.runtimeId,
            wmOpsWorkstationMetricStatusID: this.workhubContextTask.process.runtimeId
        },
        storeMetaData: {
            branchCode: this.workhubContextTask.account.entityCode,
            docSourceSystem: 'WM_CHECKLIST',
            docTargetSystem: this._resource.getContextValue('isGvaUser') === true ? 'CDS' : 'CONTENT_CLOUD',
            docTypeCode: this._resource.getContextValue('isGvaUser') === true ? 'CED' : 'EVIDENCE',
            uploadSid: this.workhubContextRequest.loggedInUser.sid,
            ticketNumber: this.workhubContextTask.ticketId
        }
    });

    formData.append('documentInfo', aa);
    formData.append('fileStream', file);

    this._dataService.postWithCallBack(new PostParameters(
        this.documentUrl,
        '/uploadFileSaveMetadata',
        { body: formData },
        'Uploading document...',
        'checklistPreviewLoader',
        this.getAllDocumentSuccess,
        (error) => {
            console.log('Document upload failed', error);
        }
    ));
}
