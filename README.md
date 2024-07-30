import { Component, OnInit, TemplateRef, ViewChild } from '@angular/core';
import { GlobalResourceService, UxcAlertService, UxcModalService } from '@connectcore/connect-components-angular';
import { DatePipe, Location } from '@angular/common';
import { ActivatedRoute, ParamMap } from '@angular/router';
import { GridOptions } from 'ag-grid-community';
import { switchMap } from 'rxjs/operators';
import { DataService } from '../../services/data.service';
import { PostParameters } from '../../models/PostParameters';
import { GetParameters } from '../../models/GetParameters';
import { ColumnDefsService } from '../../services/column-defs.service';
import { TicketAttribute } from '../../models/ticketAttribute';
import { ConnectContextService } from '@connectcore/connect-components-angular/connect';
import * as constants from '../../constants/app-constants';
import { FavMetricsService } from '../../services/fav-metrics.service';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.scss']
})
export class HomeComponent implements OnInit {

  constructor(
    private _modalService: UxcModalService,
    private columnDefService: ColumnDefsService,
    private _dataService: DataService,
    private _resource: GlobalResourceService,
    protected _location: Location,
    private route: ActivatedRoute,
    private _alertService: UxcAlertService,
    private _glueConnectService: ConnectContextService,
    private favMetrics: FavMetricsService
  ) { }

  theme = 'light';
  maxFileSizeLimit = 25;
  duplicateModalAction: string;
  showAddComments = false;
  showPage = true;
  canClaimFalseMessage = '';
  disableReject = false;
  disableApprove = false;
  redDueDate = false;
  showMarkAsComple = false;
  showApproveOrReject = false;
  disableMarkAsComplete = false;
  documentCommentDisable = false;
  attributeResponse: TicketAttribute = new TicketAttribute();
  entitlementMap: any = { markAsComplete: 'WorkHubChecklistSubmit', approveOrReject: 'WorkHubChecklistVerify' };
  showApproveReject = false;
  showMarkAsCompleteButton = false;
  showUploadDocAndAddComment = true;
  reasonForReject = '';
  maxDocumentsLimit = 2;  // Set the limit for documents
  @ViewChild('rejectModalTemplate', { static: false }) rejectModalTemplate: TemplateRef<any>;
  @ViewChild('deleteModalTemplate', { static: false }) deleteModalTemplate: TemplateRef<any>;
  loggedInUserSid: string;
  loggedInUserName: string;
  commentsGridOptions: GridOptions;
  documentsGridOptions: GridOptions;
  workhubContextRequest;
  workhubContextTask;
  comments: any[] = [];
  document;
  documents: any[] = [];
  documentUrl: any;
  commentUrl: any;
  commentsGridColumnDefs = this.columnDefService.commentColDefs;
  documentGridColumnDefs = this.columnDefService.documentsColDefs;
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
    this.showAddComments = false;
    this.comment = '';
  }

  closeWindow() {
    window.close();
  }

  createAlert(msg) {
    this._alertService.createAlertOnBody({
      message: msg,
      type: 'info',
      dismissable: true,
      position: 'top',
      dismissOnTimeout: 2000
    });
  }

  createSuccessAlert(msg) {
    this._alertService.createAlertOnBody({
      message: msg,
      type: 'success',
      dismissable: true,
      position: 'top',
      dismissOnTimeout: 3000
    });
  }

  createErrorAlert(msg) {
    this._alertService.createAlertOnBody({
      message: msg,
      type: 'danger',
      dismissable: true,
      position: 'top',
      dismissOnTimeout: 5000
    });
  }

  approveChecklistButtonClicked(type) {
    if (this.showTriggerQuestion === true && this.triggeredQuestionValue === '') {
      this.createAlert('Please answer trigger question');
    } else {
      console.log('disable mark as completed::before', this.disableMarkAsComplete);
      if (type === 'markascomplete') {
        this.disableMarkAsComplete = true;
      }
      console.log('disable mark as completed::after', this.disableMarkAsComplete);
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
              conditionalActionCode: this.showTriggerQuestion ? 'conditionalActionCode' : '',
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
            }
          },
          (error) => {
            // Handle error
          }
        )
      );
    }
  }

  rejectChecklistButtonClicked() {
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
              conditionalActionCode: '',
              conditionalActionValue: '',
            }
          },
          'Rejecting ticket...',
          'checklistPreviewLoader',
          (data) => {
            if (data.code === 200) {
              this.createAlert('Ticket is rejected successfully.');
              this.disableReject = true;
              this.disableApprove = true;
              this.disableMarkAsComplete = true;
              this.documentCommentDisable = true;
              setTimeout(() => {
                window.close();
              }, 2000);
            } else {
              console.log('Response when code not equal to 0: ' + JSON.stringify(data.message));
            }
          },
          (error) => {
            // Handle error
          }
        );
    });
  }

  // Upload document
  onFileChange(event) {
    const files = event.target.files;
    if (files.length > 0) {
      if (this.documents.length >= this.maxDocumentsLimit) {
        this.createAlert('Document limit exceeded. You can only upload up to 2 documents.');
        return;
      }

      const file = files[0];
      if (file.size / 1024 / 1024 > this.maxFileSizeLimit) {
        this.createErrorAlert('File size exceeds 25MB.');
        return;
      }

      this.uploadedfile = file;
      this.documents.push({
        name: file.name,
        size: file.size,
        type: file.type,
        url: URL.createObjectURL(file)
      });
      // Handle file upload here (e.g., send to server)
    }
  }

  // Add comments
  addComments() {
    if (this.comment) {
      this.comments.push({
        text: this.comment,
        date: new Date()
      });
      this.comment = '';
      // Handle comment submission to server if needed
    }
  }

  ngOnInit() {
    this.route.paramMap.pipe(
      switchMap((params: ParamMap) => {
        this.loggedInUserSid = this._glueConnectService.getUserSid();
        this.loggedInUserName = this._glueConnectService.getUserName();
        return this._dataService.getParameters(new GetParameters('/getParametersUrl'));
      })
    ).subscribe(
      (response) => {
        // Handle the response
      },
      (error) => {
        // Handle error
      }
    );
  }
}
