 getDocuments() {
    this._dataService.get(new GetParameters(this.documentUrl, '/get/mws/process/' + this.workhubContextTask.process.runtimeId, {body: {}}, '', '')).subscribe((data) => {
      if (data) {


        // setTimeout(()=>{
        const documentsList = data.response;
        console.log('getdocuments:documentsList',documentsList);
        if (this.attributeResponse.makerCheckerActivityList != null) {
          const activityIdList = this.attributeResponse.makerCheckerActivityList.map( activity => activity.activityId );
          console.log('getdocuments:activityIdList',activityIdList);
          this.documents = documentsList.filter( doc => activityIdList.includes(doc.mws_actv_id));
          console.log('getdocuments:this.documents',this.documents);
        }
        this.documents.forEach((document) => {
          if (((document.updt_sid).includes(this.loggedInUserSid) || this.attributeResponse.hasCheckerRole) && (this.workhubContextTask.status.code !== 'Complete')) {
            document.deleteIcon = true;
          } else {
            document.deleteIcon = false;
          }
        });
        this.documentsGridOptions.api.setRowData(this.documents);
        this.documentsGridOptions.api.sizeColumnsToFit();
        //  },3000);

        if (this.showMarkAsCompleteButton) {
          // we will try to disable mark as complete only if mark as complete button is viible.
          if (this.workhubContextTask.activity.code.toLowerCase().indexOf('checker') === -1 && this.attributeResponse && this.attributeResponse.taskDetails && this.attributeResponse.taskDetails.isEvidencingRequired === 'Y' && this.documents.length === 0) {
            this.disableMarkAsComplete = true;
          } else {
            this.disableMarkAsComplete = false;
          }
        }
        if (this.showApproveReject) {
          if (this.workhubContextTask.activity.code.toLowerCase().indexOf('checker') !== -1 && this.attributeResponse.taskDetails.isEvidencingRequired === 'Y' && this.documents.length === 0) {
            this.disableApprove = true;
            this.disableReject = false;
          } else {
            this.disableApprove = false;
            this.disableReject = false;
          }
        }
      }
    });

  }
