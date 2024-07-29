  fileChange(event) {

    console.log(event , event[event.length - 1 ]);
    if (event[event.length - 1 ].size > constants.maxFileSize || event[event.length - 1 ].size === 0) {
      this.createErrorAlert('File size should be minimum 1 Byte or maximum 25 MB');
    } else {
      if (!this.documentCommentDisable) {
        this.uploadFile(event[event.length - 1 ]);
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
      }
    );
    formData.append('documentInfo', aa);
    formData.append('fileStream', file);
    // formData.append('docCode', doc.description.documentTypeCode);
    // formData.append('comment', doc.commentText || '');
    // formData.append('team', doc.authorTeam || '');
    // formData.append('stage', doc.stage || '');
    this._dataService.postWithCallBack(new PostParameters( this.documentUrl, '/uploadFileSaveMetadata',
      {
        body: formData

      }  ,
      'Uploading  document...',
      'checklistPreviewLoader',
      this.getAllDocumentSuccess,

      (error) => {
        console.log('document upload failed error');
      }));
  }
