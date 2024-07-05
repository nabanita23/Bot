export enum NavDataValue {
  ENV = 'env',
  ACTIVITY_ID = 'activityId',
  ACTIVITY_TYPE_CODE = 'activityTypeCode',
  ACTIVITY_STS = 'activityStatus',
  TASK_DISPLAY_NAME = 'activityDisplayName',
  TASK_DESCRIPTION = 'activityDesc',
  RAG_STATUS = 'ragSts',
  TASK_DUE_DATE = 'taskDueDate',
  TASK_START_DATE = 'taskStartDate',
  TICKET_ID = 'caseId',
  PROCESS_ID = 'processId',
  PROCESS_STS = 'processStatus',
  INITIATOR_SID = 'initiatorSid',
  INITIATOR_NAME = 'initiatorName',
  ASSIGNEE_SID = 'assigneeSid',
  ASSIGNEE_NAME = 'assigneeName',
  OWNER_SID = 'ownerSid',
  OWNER_NAME = 'ownerName',
  LOGGED_IN_SID = 'loggedInUserSid',
  OWNER_TEAM_CD = 'owningTeamCode',
  OWNER_TEAM_NAME = 'owningTeamName',
  CATEGORY = 'categoryDesc',
  REQUEST_TYPE = 'requestTypeDesc',
  REQUEST_SUB_TYPE = 'requestSubTypeDesc',
  ECI = 'eci',
  GWM_ID = 'gwmId',
  ACC_NO = 'accountNumber',
  BUS_SYS_CD = 'businessSystemCode',
  UNMASKED_CLIENT_NAME = 'clientName',
  MASKED_CLIENT_NAME = 'maskedClientName',
  ENTITY_CODE = 'entityCode',
}

const latestActivity = response?.latestActivityResponse[0];

  navData[NavDataValue.ACTIVITY_ID] = navData[NavDataValue.ACTIVITY_ID] ?? latestActivity?.id
  navData[NavDataValue.ACTIVITY_TYPE_CODE] = navData[NavDataValue.ACTIVITY_TYPE_CODE] ?? latestActivity?.taskDefinitionKey
  navData[NavDataValue.TASK_DISPLAY_NAME] = navData[NavDataValue.TASK_DISPLAY_NAME] ?? latestActivity?.name
  navData[NavDataValue.TASK_START_DATE] = navData[NavDataValue.TASK_START_DATE] ?? latestActivity?.created
      ? dateformat(new Date(latestActivity?.created), 'dd mmm yyyy h:MM TT')
      : null
  navData[NavDataValue.TASK_DUE_DATE] = navData[NavDataValue.TASK_DUE_DATE] ?? latestActivity?.due
      ? dateformat(new Date(latestActivity?.due), 'dd mmm yyyy h:MM TT')
      : null
    navData[NavDataValue.ACTIVITY_TYPE_CODE] = latestActivity?.taskDefinitionKey
  navData[NavDataValue.PROCESS_ID] = navData[NavDataValue.PROCESS_ID] ?? latestActivity?.processInstanceId
  navData[NavDataValue.PROCESS_STS] = navData[NavDataValue.PROCESS_STS] ?? latestActivity?.processStatus
  navData[NavDataValue.INITIATOR_SID] = navData[NavDataValue.INITIATOR_SID] ?? latestActivity?.initiatorSid
  navData[NavDataValue.INITIATOR_NAME] = navData[NavDataValue.INITIATOR_NAME] ?? latestActivity?.initiatorName
  navData[NavDataValue.ASSIGNEE_NAME] = latestActivity?.assigneeName
  navData[NavDataValue.ASSIGNEE_SID] = latestActivity?.assigneeSid
  navData[NavDataValue.OWNER_NAME] = latestActivity?.ownerName
  navData[NavDataValue.OWNER_SID] = latestActivity?.ownerSid
  navData[NavDataValue.OWNER_TEAM_CD] = navData[NavDataValue.OWNER_TEAM_CD] ?? latestActivity?.teamCode
  navData[NavDataValue.OWNER_TEAM_NAME] = navData[NavDataValue.OWNER_TEAM_NAME] ?? latestActivity?.teamName
  navData[NavDataValue.ECI] = navData[NavDataValue.ECI] ?? latestActivity?.eci
  navData[NavDataValue.ACC_NO] = navData[NavDataValue.ACC_NO] ?? latestActivity?.accountNumber
  navData[NavDataValue.ENTITY_CODE] = navData[NavDataValue.ENTITY_CODE] ?? latestActivity?.entityCode
