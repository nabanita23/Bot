import {Component, OnInit, TemplateRef, ViewChild} from '@angular/core';
import {GlobalResourceService, UxcAlertService, UxcModalService} from '@connectcore/connect-components-angular';
import {DatePipe, Location} from '@angular/common';
import {ActivatedRoute, ParamMap} from '@angular/router';
import {GridOptions} from 'ag-grid-community';
import {switchMap} from 'rxjs/operators';
import {DataService} from '../../services/data.service';
import {PostParameters} from '../../models/PostParameters';
import {GetParameters} from '../../models/GetParameters';
import {ColumnDefsService} from '../../services/column-defs.service';
import {TicketAttribute} from '../../models/ticketAttribute';
import {ConnectContextService} from '@connectcore/connect-components-angular/connect';
import * as constants from '../../constants/app-constants';
import {FavMetricsService} from '../../services/fav-metrics.service';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.scss']
})
export class HomeComponent implements OnInit {
  constructor( private _modalService: UxcModalService, private columnDefService: ColumnDefsService  , private _dataService: DataService,
               private _resource: GlobalResourceService, protected _location: Location, private route: ActivatedRoute,
               private _alertService: UxcAlertService, private _glueConnectService: ConnectContextService, private favMetrics: FavMetricsService) {
  }
  theme = 'light';
  maxFileSizeLimit = 25;
  duplicateModalAction: string;
  showAddComments  = false;
  showPage  = true;
  canClaimFalseMessage = '';
  disableReject  = false;
  disableApprove  = false;
  redDueDate  = false;
  showMarkAsComple  = false;
  showApproveOrReject  = false;
  disableMarkAsComplete  = false;
  documentCommentDisable = false;
  attributeResponse: TicketAttribute = new TicketAttribute();
  entitlementMap: any = {
    markAsComplete: 'WorkHubChecklistSubmit',
    approveOrReject: 'WorkHubChecklistVerify'
  };
  showApproveReject  = false;
  showMarkAsCompleteButton  = false;
  showUploadDocAndAddComment  = true;
  reasonForReject = '';
  @ViewChild('rejectModalTemplate', {static: false}) rejectModalTemplate: TemplateRef<any>;
  @ViewChild('deleteModalTemplate', {static: false}) deleteModalTemplate: TemplateRef<any>;
  loggedInUserSid: string;
  loggedInUserName: string;
  commentsGridOptions: GridOptions;
  documentsGridOptions: GridOptions;
  workhubContextRequest;
  workhubContextTask;
  comments: any[] = [];
  document;
  documents: any[] = [];
  documentUrl :any;
  commentUrl:any;
  commentsGridColumnDefs =  this.columnDefService.commentColDefs;
  documentGridColumnDefs =  this.columnDefService.documentsColDefs;
  uploadedfile: File = null;
  comment;
  controlIdValue;
  showTriggerQuestion = false;
  triggeredQuestionValue = '';
  triggeredQuestionOptions = [
    { lookupCode: 'yes', lookupValue: 'Yes' },
    { lookupCode: 'no', lookupValue: 'No' },
  ];
  setTheme(theme: string): void {
    this.theme = theme;
    document.documentElement.className = theme;
  }
  showCommentsGrid() {
    this.showAddComments = true;
  }
  cancelAddComments() {
    this.showAddComments = false; this.comment = '';
  }
  closeWindow() {
    window.close();
  }
  createAlert(msg) {
    this._alertService.createAlertOnBody(
      {
        message: msg,
        type: 'info',
        dismissable: true,
        position: 'top',
        dismissOnTimeout: 2000
      }
    );
  }
  createSuccessAlert(msg) {
    this._alertService.createAlertOnBody(
      {
        message: msg,
        type: 'success',
        dismissable: true,
        position: 'top',
        dismissOnTimeout: 3000
      }
    );
  }
  createErrorAlert(msg) {
    this._alertService.createAlertOnBody(
      {
        message: msg,
        type: 'danger',
        dismissable: true,
        position: 'top',
        dismissOnTimeout: 5000
      }
    );
  }
  approveChecklistButtonClicked(type) {
    // if (this.attributeResponse.taskDetails.triggeredQuestion !== '' && this.triggeredQuestionValue === '' && this.workhubContextTask.activity.code.toLowerCase().indexOf('checker') >= 0 && this.attributeResponse.taskDetails.isParentTask === 'Y') {
    if (this.showTriggerQuestion === true && this.triggeredQuestionValue === '') {
      this._alertService.createAlertOnBody(
        {
          message: 'Please answer trigger question',
          type: 'danger',
          dismissable: true,
          position: 'top',
          dismissOnTimeout: 3000
        }
      );
    } else {
      console.log('disable mark as completed::before',this.disableMarkAsComplete);
      if(type === 'markascomplete') {
        this.disableMarkAsComplete = true;
      }
      console.log('disable mark as completed::after',this.disableMarkAsComplete);
      this._dataService.postWithCallBack(
        new PostParameters(
          this._resource.getContextValue('checklistServiceEndPoints')[this.workhubContextRequest.activeProfile],
          '/workflow/completeActivity',
          {
            body: {
              accountNumber: this.workhubContextTask.account.number,
              entityCode: this.workhubContextTask.account.entityCode,
              currentOwnerFunction: type === 'markascomplete' ? this.entitlementMap.markAsComplete : this.entitlementMap.approveOrReject,
              activityId: this.workhubContextTask.activity.runtimeId,
              activityStatus: this.workhubContextTask.status.code,
              activityTypeCode: this.workhubContextTask.activity.code,
              activityTypeDesc: this.workhubContextTask.activity.description,
              busSysCd: this.workhubContextTask.account.businessSystemCode,
              caseId: this.workhubContextTask.ticketId,
              caseStatus: '',
              eci: this.workhubContextTask.client.eci,
              error: '',
              hierarchyId: this.workhubContextRequest.hierarchyId,
              initiatingTeamCd: this.workhubContextTask.initiatingTeam.code,
              initiatorSid: this.workhubContextTask.initiator.sid,
              loggedInSid: this.workhubContextRequest.loggedInUser.sid,
              mwsResponseCode: '',
              mwsResponseMessage: '',
              ownerSid: this.workhubContextTask.owner.sid,
              owningTeamCd: this.workhubContextTask.owningTeam.code,
              processDefinitionName: '',
              processId: this.workhubContextTask.process.runtimeId,
              slaMillis: '',
              targetOwnerFunction: '',
              targetOwnerSid: '',
              targetTeamCd: this.workhubContextTask.owningTeam.code,
              workflowActionKey: 'actionCode',
              workflowActionValue: 'approve',
              conditionalActionCode : this.showTriggerQuestion ? 'conditionalActionCode' : '',
              conditionalActionValue: this.showTriggerQuestion ? this.triggeredQuestionValue : '',
            }
          },
          type === 'approve' ? 'Approving ticket...' : 'Submitting ticket...',
          'checklistPreviewLoader',
          (data) => {
            const response = data.code;
            if (response === 200) {
              if (type === 'approve') {
                this.favMetrics.logMetric('WorkHub Checklist Action', 'Approve');
              } else {
                this.favMetrics.logMetric('WorkHub Checklist Action', 'Mark Complete');
              }
              type === 'approve' ? this.createAlert('Ticket is approved successfully') : this.createAlert('Action successful.');
              this.disableApprove = true;
              this.disableReject = true;
              this.disableMarkAsComplete = true;
              this.documentCommentDisable = true;
              setTimeout(() => {
                window.close();
              }, 2000);
            } else {
              console.log('Response when code not equal to 0: ' + JSON.stringify(data.message));
              // this.createAlert(data.message);
              // this.createAlert(data.message + ' with trace id = ' + data.traceId);
            }
          },
          (error) => {

          }
        ));
    }

  }

  rejectChecklistButtonClicked() {
    // if (this.reasonForReject != null) {
    //   this.comment = this.reasonForReject;
    // }
    const modalInstance = this._modalService.openModal('body', this.rejectModalTemplate, {});
    modalInstance.on('reject', (context) => {
      this.comment = this.reasonForReject;
      this.reasonForReject = '';
      this.addComments();
      this.duplicateModalAction = context;
      this._dataService.postWithCallBack(
        new PostParameters(
          this._resource.getContextValue('checklistServiceEndPoints')[this.workhubContextRequest.activeProfile],
          '/workflow/completeActivity',
          {
            body: {
              accountNumber: this.workhubContextTask.account.number,
              currentOwnerFunction: this.entitlementMap.approveOrReject,
              entityCode: this.workhubContextTask.account.entityCode,
              activityId: this.workhubContextTask.activity.runtimeId,
              activityStatus: this.workhubContextTask.status.code,
              activityTypeCode: this.workhubContextTask.activity.code,
              activityTypeDesc: this.workhubContextTask.activity.description,
              busSysCd: this.workhubContextTask.account.businessSystemCode,
              caseId: this.workhubContextTask.ticketId,
              caseStatus: '',
              eci: this.workhubContextTask.client.eci,
              error: '',
              hierarchyId: this.workhubContextRequest.hierarchyId,
              initiatingTeamCd: this.workhubContextTask.initiatingTeam.code,
              initiatorSid: this.workhubContextTask.initiator.sid,
              loggedInSid: this.workhubContextRequest.loggedInUser.sid,
              mwsResponseCode: '',
              mwsResponseMessage: '',
              ownerSid: this.workhubContextTask.owner.sid,
              owningTeamCd: this.workhubContextTask.owningTeam.code,
              processDefinitionName: '',
              processId: this.workhubContextTask.process.runtimeId,
              slaMillis: '',
              targetOwnerFunction: '',
              targetOwnerSid: '',
              targetTeamCd: this.workhubContextTask.owningTeam.code,
              workflowActionKey: 'actionCode',
              workflowActionValue: 'reject',
            }
          },
          'Rejecting ticket...',
          'checklistPreviewLoader',
          (data) => {


            const response = data.code;
            if (response === 200) {
              this.favMetrics.logMetric ('WorkHub Checklist Action', 'Reject');
              this.createAlert('Ticket is rejected successfully');
              this.disableApprove = true;
              this.disableReject = true;
              this.disableMarkAsComplete =  true;
              this.documentCommentDisable = true;
              setTimeout(() => {
                window.close();
              }, 2000);
            } else {
              console.log('Response when code not equal to 0: ' + JSON.stringify(data.message));
              // this.createAlert(data.message + ' with trace id = ' + data.traceId);
            }
          },
          (error) => {

          }
        ));
    });

    modalInstance.on('cancel', (context) => {
      this.duplicateModalAction = context;
      this.reasonForReject = '';

    });

  }
  rejectChecklistSuccess(data) {

  }
  rejectChecklistFailure() {

  }
  handleFileInput(files: FileList) {
    console.log(files);
    // this.uploadedfile = files.item(0);
    // this.uploadFile(files.item(0));
  }
  fileChange(event) {

    console.log('test',event , event[event.length - 1 ].length);
    if (event[event.length - 1 ].size > constants.maxFileSize || event[event.length - 1 ].size === 0) {
      this.createErrorAlert('File size should be minimum 1 Byte or maximum 25 MB');
    } else {
      if (!this.documentCommentDisable) {
        this.uploadFile(event[event.length - 1 ]);
      }
    }

  }
  uploadFile(file) {
    console.log('testing',file, this.uploadedfile);


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
  openDeleteConfirmationModal(comment) {
    this.deleteComment(comment);
  }
  deleteComment(comment) {

    setTimeout(() => {
      this._dataService.postWithCallBack(new PostParameters(this.commentUrl, '/deactivate',
        { body: {
            actionCode: 'DEL',
            activeFlag: comment.activeFlag,
            commentId: comment.commentId,
            commentText: comment.commentText,
            commentType: comment.commentType,
            createTimestamp: comment.createTimestamp,
            createdSid: comment.createdSid,
            mwsActivityId: comment.mwsActivityId,
            mwsProcessId: comment.mwsProcessId,
            updateTimestamp: comment.updateTimestamp,
            updatedSid: comment.updatedSid
          } },
        'Fetching all checklists ...',
        'serviceCallLoader',
        this.getAllSuccess,

        this.getAllSuccess));
    }, 1000);

  }
  openDocumentDeleteConfirmationModal(document) {
    console.log('document data', document);
    this.document = document;
    const modalInstance = this._modalService.openModal('body', this.deleteModalTemplate, {});
    modalInstance.on('cancel', (context) => {
      // this.confirmModalAction = 'cancel';
    });
    modalInstance.on('delete', (context) => {
      this._dataService.postWithCallBack(
        new PostParameters(
          this.documentUrl,'/deleteFile?specificDocumentMetaData=%7B%22targetSystemDocumentReference%22%3A' + document.trgt_sys_doc_ref + '%2C%22wmOpsWorkstationMetricStatusID%22%3A' + document.mws_prcs_id + '%2C%22wmOpsWorkstationID%22%3A' + document.mws_actv_id + '%7D',
          // '/deleteFile?specificDocumentMetaData={"targetSystemDocumentReference":"' + document.trgt_sys_doc_ref + '","wmOpsWorkstationMetricStatusID":"' + document.mws_prcs_id + '","wmOpsWorkstationID":' + document.mws_actv_id + '}',
          {
            body: {}
          },
          'Deleting document ...',
          '',
          (data) => {
            this.createSuccessAlert ('Deleted the document successfully');
            this.getDocuments();
          },
          (error) => {
            console.log('error');
          }
        )
      );
    });
  }


  getAllDocumentSuccess = (data: any) => {
    this.favMetrics.logMetric ('WorkHub Checklist Action', 'Add attachment');
    console.log('allWorkflow data from endpoint', data);
    this.getDocuments();
  }
  getAllSuccess = (data: any) => {
    console.log('allWorkflow data from endpoint', data);
    this.getComments();
    this.showAddComments = false;
    this.comment = '';
  }

  initializeCommentsGrid() {
    this.documentsGridOptions = {
      // domLayout:'autoHeight',
      groupUseEntireRow: true,
      // groupDefaultExpanded: -1,
      // groupSuppressBlankHeader: true,
      // groupHideOpenParents: true,
      animateRows: true,
      singleClickEdit: true,
      defaultColDef: {
        filter: true,
        sortable: true,
        resizable: true,
        enableRowGroup: true,
        tooltipValueGetter(params) {
          return params.value;
        }
      },
      sideBar: {
        toolPanels: [{
          id: 'columns',
          labelDefault: 'Columns',
          labelKey: 'columns',
          iconKey: 'columns',
          toolPanel: 'agColumnsToolPanel',
          toolPanelParams: {
            suppressRowGroups: false,
            suppressValues: true,
            suppressPivots: true,
            suppressPivotMode: true,
            suppressColumnSelectAll: true
          }
        }]
      },
      rowData: [],
      rowHeight: 30,
      columnDefs: this.documentGridColumnDefs,
      suppressDragLeaveHidesColumns: true,
      headerHeight: 30,
      statusBar: {
        statusPanels: [
          {
            statusPanel: 'agTotalRowCountComponent',
            align: 'right'
          },
          { statusPanel: 'agFilteredRowCountComponent' },
          { statusPanel: 'agSelectedRowCountComponent' },
          { statusPanel: 'agAggregationComponent' }
        ]
      },
      context: {
        componentParent: this,
      },
      onRowClicked: params => {
        console.log('row selection called ');
        // this.openPreviewScreen(params.data);
      },
      onGridReady: params => {
        this.documentsGridOptions.api = params.api;
        this.documentsGridOptions.api.sizeColumnsToFit();
      },
      onGridSizeChanged: params => {
        // if(!this.previewScreen)
        this.documentsGridOptions.api.sizeColumnsToFit();
      }
    };
    this.commentsGridOptions = {
      // domLayout:'autoHeight',
      groupUseEntireRow: true,
      // groupDefaultExpanded: -1,
      // groupSuppressBlankHeader: true,
      // groupHideOpenParents: true,
      animateRows: true,
      context: {
        componentParent: this,
      },
      singleClickEdit: true,
      defaultColDef: {
        filter: true,
        sortable: true,
        resizable: true,
        enableRowGroup: true,
        tooltipValueGetter(params) {
          return params.value;
        }
      },
      sideBar: {
        toolPanels: [{
          id: 'columns',
          labelDefault: 'Columns',
          labelKey: 'columns',
          iconKey: 'columns',
          toolPanel: 'agColumnsToolPanel',
          toolPanelParams: {
            suppressRowGroups: false,
            suppressValues: true,
            suppressPivots: true,
            suppressPivotMode: true,
            suppressColumnSelectAll: true
          }
        }]
      },
      rowData: [],
      rowHeight: 30,
      columnDefs: this.commentsGridColumnDefs,
      suppressDragLeaveHidesColumns: true,
      headerHeight: 30,
      statusBar: {
        statusPanels: [
          {
            statusPanel: 'agTotalRowCountComponent',
            align: 'right'
          },
          { statusPanel: 'agFilteredRowCountComponent' },
          { statusPanel: 'agSelectedRowCountComponent' },
          { statusPanel: 'agAggregationComponent' }
        ]
      },
      onRowClicked: params => {
        console.log('row selection called ');
        // this.openPreviewScreen(params.data);
      },
      onGridReady: params => {
        this.commentsGridOptions.api = params.api;
        this.commentsGridOptions.api.sizeColumnsToFit();
      },
      onGridSizeChanged: params => {
        // if(!this.previewScreen)
        this.commentsGridOptions.api.sizeColumnsToFit();
      }
    };
  }

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

  getComments() {

    this._dataService.get(new GetParameters(this.commentUrl, '/get/mws/process/' + this.workhubContextTask.process.runtimeId + '/Y', {body: {}}, '', '')).subscribe((data) => {
      const commentList = [];
      if (data && data.response) {
        data.response.map(comment => {
          if (comment.activeFlag === 'Y') {
            console.log('comment',comment);
            commentList.push(comment);
          }
        });
        // setTimeout(()=>{
        if (this.attributeResponse.makerCheckerActivityList != null) {
          const activityIdListComment = this.attributeResponse.makerCheckerActivityList.map( activity => activity.activityId );
          console.log('activityIdListComment',activityIdListComment);
          this.comments = commentList.filter( comment => activityIdListComment.includes(comment.mwsActivityId));
          console.log('commentList',commentList);
          console.log('this.comments',this.comments);
        }
        this.commentsGridOptions.api.setRowData(this.comments);
        this.commentsGridOptions.api.sizeColumnsToFit();
        // },5000);

      }
    });
  }
  addComments() {
    this.favMetrics.logMetric ('WorkHub Checklist Action', 'Add comment');
    this._dataService.postWithCallBack(new PostParameters(this.commentUrl, '/add',
      { body: {
          actionCode: 'ADD',
          activeFlag: 'Y',
          commentId: 0,
          commentText: this.comment,
          commentType: 'CHECKLIST',
          createTimestamp: '',
          createdSid: this.loggedInUserSid,
          mwsActivityId: this.workhubContextTask.activity.runtimeId,
          mwsProcessId: this.workhubContextTask.process.runtimeId,
          updateTimestamp: '',
          updatedSid: this.loggedInUserSid
        } },
      'Adding comment ...',
      'checklistCommentsLoader',
      this.getAllSuccess,

      () => {
        this.showAddComments = false;
        this.comment = '';
      }));
  }


  postGlueInit() {
    this._glueConnectService.glue.activities
      .ready()
      .then(api => this.activityInitialized(api.my.context));
    this.subscribeToConnectTheme();
  }  activityInitialized(context) {
  }  subscribeToConnectTheme() {
    this.getInitialConnectTheme();
    this._glueConnectService.subscribeToMethod('Connect.ChangeTheme').subscribe((p: any) => {
      console.log('Value From My.Connect.AGM.Method', p);
      if (p) {
        console.log('connect change theme', JSON.parse(JSON.stringify(p)));
        this.setTheme(p.theme);
      }
    });
  }  getInitialConnectTheme() {
    this._glueConnectService.invokeMethod('GWM.Global.GetCurrentTheme', {   }, 'best', {}, (res) => {
      console.log('inside connect initial theme', JSON.parse(JSON.stringify(res)));
      this.setTheme(res.returned.theme);
    });
    this._glueConnectService.invokeMethod('GWM.AppManager.CheckGenevaAccess', {   }, 'best', {}, (res) => {
      this._resource.setContextValue('isGvaUser', res.returned.inGenevaAndHasGenevaAccess);
      this.initializeContext();
      // if(res.returned.inGenevaAndHasGenevaAccess) {
      //  console.log('gva user');
      //   this._resource.setContextValue('isGvaUser', true);
      //   this.documentUrl = (this.workhubContextRequest.activeProfile === 'ipbprod') ? (this._resource.getContextValue('documentsEndPoints').gvaprod) : (this._resource.getContextValue('documentsEndPoints').gvatest);
      //   this.commentUrl = (this.workhubContextRequest.activeProfile === 'ipbprod') ? (this._resource.getContextValue('commentsEndPoints').gvaprod) : (this._resource.getContextValue('commentsEndPoints').gvatest);
      // } else {
      //   console.log('nongva user');
      //   this._resource.setContextValue('isGvaUser', false);
      //   this.documentUrl= this._resource.getContextValue('documentsEndPoints')[this.workhubContextRequest.activeProfile];
      //   this.commentUrl= this._resource.getContextValue('commentsEndPoints')[this.workhubContextRequest.activeProfile];
      // }
    });
  }

  ngOnInit() {
    this._glueConnectService.ready().subscribe(() => {
      // Start using the connect context service here
      this.postGlueInit();
    });
    this.initializeCommentsGrid();
    // this.initializeContext();
    // this.getDocuments();
    // this.getComments();
    //   this.initializeAndCallCommentsAndDocsService();
    // this.getWeaveEntitlements();

  }
  initializeAndCallCommentsAndDocsService() {
    // this.initializeCommentsGrid();
    this.getDocuments();
    this.getComments();
  }
  initializeAttributes() {
    // if( new Date().getTime() >   Number(this.attributeResponse.dueDateMillis)){
    //   this.redDueDate = true;
    // }else{
    //   this.redDueDate = false;
    // }
    // console.log(this._resource.getContextValue('checklistServiceEndPoints')[this.workhubContextRequest.activeProfile]);
    // console.log( this._resource.getContextValue('checklistServiceEndPoints'));
    this._dataService.postWithCallBack(
      new PostParameters(
        this._resource.getContextValue('checklistServiceEndPoints')[this.workhubContextRequest.activeProfile],
        '/workflow/getHeaderAttributes',
        {
          body: {
            caseId: this.workhubContextTask.ticketId,
            activityId: this.workhubContextTask.activity.runtimeId,
            processId: this.workhubContextTask.process.runtimeId,
            activityTypeCode: this.workhubContextTask.activity.code,
            hierarchyId: this.workhubContextRequest.hierarchyId,
            loggedInSid: this.workhubContextRequest.loggedInUser.sid ,
            entityCode: this.workhubContextTask.account.entityCode,
            owningTeamCd: this.workhubContextTask.owningTeam.code,
            activityDisplayName : this.workhubContextTask.activity.displayName
          }
        },
        'Fetching ticket details...',
        'checklistPreviewLoader',
        (data) => {
          this.showMarkAsCompleteButton=true;
          this.attributeResponse = data.response;
          console.log(this.attributeResponse);
          this.controlIdValue = this.attributeResponse.taskDetails.controlId === 0 ? '---' : this.attributeResponse.taskDetails.controlId;
          if (this.attributeResponse && this.attributeResponse.processStatus && (this.attributeResponse.processStatus.toLowerCase() === 'complete' || this.attributeResponse.processStatus.toLowerCase() === 'abandoned')) {
            this.showApproveReject = false;
            this.showMarkAsCompleteButton = false;
            this.showUploadDocAndAddComment =  false;
            if (this.attributeResponse && this.attributeResponse.historicalReadAllowed ) {
              this.showPage = true;
              this.initializeAndCallCommentsAndDocsService();
            } else {
              this.showPage = false;
              this.canClaimFalseMessage = 'You are not entitled to view this page.';
            }
          } else {
            if (this.workhubContextTask.canClaim === 'Y' && this.attributeResponse.teamEntityCheck) {
              this.showPage = true;
              if (this.workhubContextTask.activity.code.toLowerCase().indexOf('checker') !== -1 && this.attributeResponse.hasCheckerRole) {
                this.showApproveReject = true;
                this.showMarkAsCompleteButton = false;
              }
              this.initializeAndCallCommentsAndDocsService();
            } else {
              this.showPage = false;
              if (this.workhubContextTask && this.workhubContextTask.owner && this.workhubContextTask.owner.sid && this.workhubContextTask.owner.sid !== this.loggedInUserSid && this.attributeResponse.teamEntityCheck) {
                this.canClaimFalseMessage = 'Current Owner is ' + this.workhubContextTask.owner.fullName + ' ( ' + this.workhubContextTask.owner.sid + ' ). Please change ownership to take action.';
              } else {
                this.canClaimFalseMessage = 'You are not entitled to view this page.';
              }
            }
          }
          if (this.attributeResponse.taskDetails.isParentTask === 'Y') {
            if (this.attributeResponse.taskDetails.isMakerChecker === 'Y' && this.workhubContextTask.activity.code.toLowerCase().indexOf('checker') >= 0) {
              this.showTriggerQuestion = true;
            } else if (this.attributeResponse.taskDetails.isMakerChecker === 'N' && this.workhubContextTask.activity.code.toLowerCase().indexOf('maker') >= 0) {
              this.showTriggerQuestion = true;
            } else {
              this.showTriggerQuestion = false;
            }
          } else {
            this.showTriggerQuestion = false;
          }
          if ( new Date().getTime() >   Number(this.attributeResponse.dueDateMillis)) {
            this.redDueDate = true;
          } else {
            this.redDueDate = false;
          }
        },
        (error) => {

        }
      ));
  }
  initializeContext() {
    console.log('Loading context from navigation parameter map...');
    const id = this.route.snapshot.paramMap.get('id');
    console.log(id, atob(id));
    const queryPath1 = this._location.path();
    if (true) {
      const paramsStr = atob(id);
      const keyValues = paramsStr.split('|');
      const paramMap: any = {};
      // let basePath = queryPath.substring(0, start);
      for (const keyValue of keyValues) {
        const keyValueArr = keyValue.split('=');
        if (keyValueArr.length >= 2) {
          paramMap[keyValueArr[0]] = keyValueArr[1].replace('%20', ' ');
        }
      }
      const context = {
        request: {
          loggedInUser: {
            sid: paramMap.loggedInUserSid ? paramMap.loggedInUserSid : ''
          },
          hierarchyId: paramMap.hierarchyId,
          requestSource: paramMap.pageFrom,
          activeProfile: paramMap.activeProfile ? paramMap.activeProfile : ''
        },
        task: {
          canClaim: paramMap.canClaim ? paramMap.canClaim : 'N',
          ticketId: paramMap.caseId ? paramMap.caseId : '',
          sugarCaseId: paramMap.sugarCaseId,
          largeClient: paramMap.largeClient,
          client: {
            eci: paramMap.eci,
            name: paramMap.clientName,
            gwmId: paramMap.gwmIdentifier,
          },
          account: {
            number: paramMap.accountNumber,
            entityCode: paramMap.entityCode ? paramMap.entityCode : '',
            businessSystemCode: paramMap.businessSystemCode
          },
          category: {
            description: paramMap.categoryDesc,
            code: paramMap.categoryCode
          },
          requestType: {
            description: paramMap.requestTypeDesc,
            code: paramMap.requestTypeCode
          },
          requestSubType: {
            description: paramMap.requestSubTypeDesc,
            code: paramMap.requestSubTypeCode
          },
          hierarchyId: paramMap.hierarchyId,
          initiator: {
            sid: paramMap.initiatorSid,
            fullName: paramMap.initiatorName
          },
          initiatingTeam: {
            code: paramMap.initiatingTeamCode,
            description: paramMap.initiatingTeamName
          },
          platform: paramMap.activePlatform,
          activeEnvironment: paramMap.activeEnvironment,
          process: {
            runtimeId: paramMap.processId ?  paramMap.processId : '',
            code: ''
          },
          activity: {
            runtimeId: paramMap.activityId ? paramMap.activityId : '',
            code: paramMap.activityTypeCode ? paramMap.activityTypeCode : '',
            description: paramMap.activityDisplayName ? paramMap.activityDisplayName : '',
            displayName: paramMap.activityDisplayName ? paramMap.activityDisplayName : '',
          },
          status: {
            code: paramMap.activityStatus ? paramMap.activityStatus : '',
            description: paramMap.activityStatus
          },
          owner: {
            sid: paramMap.ownerSid ? paramMap.ownerSid : '',
            fullName: paramMap.ownerName ? paramMap.ownerName : ''
          },
          owningTeam: {
            code: paramMap.owningTeamCode,
            description: paramMap.owningTeamName
          }
        }
      };
      console.log('serialized nav data', context);
      this.workhubContextRequest =  context.request;
      this.workhubContextTask =  context.task;
      if(this._resource.getContextValue('isGvaUser') === true) {
        console.log('gva user');
        this.documentUrl = (this.workhubContextRequest.activeProfile.includes('prod') ) ? (this._resource.getContextValue('documentsEndPoints').gvaprod) : (this._resource.getContextValue('documentsEndPoints').gvatest);
        this.commentUrl = (this.workhubContextRequest.activeProfile.includes('prod') ) ? (this._resource.getContextValue('commentsEndPoints').gvaprod) : (this._resource.getContextValue('commentsEndPoints').gvatest);
        this._resource.setContextValue('documentUrl', this.documentUrl);
      } else {
        console.log('nongva user');
        this.documentUrl= this._resource.getContextValue('documentsEndPoints')[this.workhubContextRequest.activeProfile];
        this.commentUrl= this._resource.getContextValue('commentsEndPoints')[this.workhubContextRequest.activeProfile];
        this._resource.setContextValue('documentUrl', this.documentUrl);
      }
      this.loggedInUserSid = paramMap.loggedInUserSid ? paramMap.loggedInUserSid : '';
      this._resource.setContextValue('loggedInUserSid', this.loggedInUserSid);
      this._resource.setContextValue('ticketId', this.workhubContextTask.ticketId);
      this._resource.setContextValue('workflowStage', this.workhubContextTask.activity.displayName);
      this._resource.setContextValue('teamName', this.workhubContextTask.owningTeam.description);
      this.loggedInUserName = this._resource.getContextValue('loggedInUserName');

      this.initializeAttributes();
      // if(this.workhubContextTask.activity.code.toLowerCase().indexOf('checker') != -1 && this.showApproveOrReject){


      // // if(this.workhubContextTask.activity.code.substr(-5).toLowerCase().indexOf('maker') != -1 && this.showMarkAsComple){
      //   if(this.workhubContextTask.activity.code.substr(-5).toLowerCase().indexOf('maker') != -1){
      //
      //   this.showMarkAsCompleButton = true;
      // }
      console.log('Final buttons mark complete', this.showMarkAsCompleteButton, this.showMarkAsComple);
      console.log('Final buttons approve or reject', this.showApproveReject, this.showApproveOrReject);
      console.log('Setting task and request objects to context....');
      this._resource.setContextValue('request', context.request);
      this._resource.setContextValue('task', context.task);



    }
  }

}
