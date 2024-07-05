const latestActivity = response?.latestActivityResponse[0];

const formatDate = (date) => date ? dateformat(new Date(date), 'dd mmm yyyy h:MM TT') : null;

const fieldsToUpdate = {
  [NavDataValue.ACTIVITY_ID]: 'id',
  [NavDataValue.ACTIVITY_TYPE_CODE]: 'taskDefinitionKey',
  [NavDataValue.TASK_DISPLAY_NAME]: 'name',
  [NavDataValue.TASK_START_DATE]: (activity) => formatDate(activity?.created),
  [NavDataValue.TASK_DUE_DATE]: (activity) => formatDate(activity?.due),
  [NavDataValue.PROCESS_ID]: 'processInstanceId',
  [NavDataValue.PROCESS_STS]: 'processStatus',
  [NavDataValue.INITIATOR_SID]: 'initiatorSid',
  [NavDataValue.INITIATOR_NAME]: 'initiatorName',
  [NavDataValue.ASSIGNEE_NAME]: 'assigneeName',
  [NavDataValue.ASSIGNEE_SID]: 'assigneeSid',
  [NavDataValue.OWNER_NAME]: 'ownerName',
  [NavDataValue.OWNER_SID]: 'ownerSid',
  [NavDataValue.OWNER_TEAM_CD]: 'teamCode',
  [NavDataValue.OWNER_TEAM_NAME]: 'teamName',
  [NavDataValue.ECI]: 'eci',
  [NavDataValue.ACC_NO]: 'accountNumber',
  [NavDataValue.ENTITY_CODE]: 'entityCode'
};

for (const [key, value] of Object.entries(fieldsToUpdate)) {
  navData[key] = navData[key] ?? (typeof value === 'function' ? value(latestActivity) : latestActivity?.[value]);
}
