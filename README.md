with Group

function getLeafComponentsGroupedByTitle(schema) {
  const groupedComponents = {};

  function traverse(components, parentTitle = "Untitled") {
    components.forEach((component) => {
      const title = component.title || parentTitle; // Use title if present, else inherit parent

      if (component.components && component.components.length > 0) {
        traverse(component.components, title);
      } else if (component.columns && component.columns.length > 0) {
        component.columns.forEach((col) => traverse(col.components || [], title));
      } else {
        if (!groupedComponents[title]) {
          groupedComponents[title] = [];
        }
        groupedComponents[title].push(component);
      }
    });
  }

  if (schema.components) {
    traverse(schema.components);
  }

  // Convert the grouped object into an array format
  return Object.keys(groupedComponents).map((title) => ({
    title,
    data: groupedComponents[title],
  }));
}
-------



function getLeafComponents(schema) {
  const leafComponents = [];

  function traverse(components) {
    components.forEach((component) => {
      if (component.components && component.components.length > 0) {
        traverse(component.components);
      } else if (component.columns && component.columns.length > 0) {
        component.columns.forEach((col) => traverse(col.components || []));
      } else {
        leafComponents.push(component);
      }
    });
  }

  if (schema.components) {
    traverse(schema.components);
  }

  return leafComponents;
}

Nabanita


{
    "bodySchema": {
        "components": [
            {
                "label": "Columns",
                "columns": [
                    {
                        "components": [
                            {
                                "label": "PID",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "input"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": true,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "pid",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "e1wi35v",
                                "defaultValue": ""
                            },
                            {
                                "label": "Party ID",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "input"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": true,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "primusPartyId",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "el6ile",
                                "defaultValue": null
                            },
                            {
                                "label": "Document Section",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": false,
                                "autofocus": true,
                                "disabled": true,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "url",
                                "data": {
                                    "values": [
                                        {
                                            "label": "",
                                            "value": ""
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "headers": [
                                        {
                                            "key": "",
                                            "value": ""
                                        }
                                    ],
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "",
                                "valueProperty": "value",
                                "template": "<span>{{ item.label }}</span>",
                                "refreshOn": "pid",
                                "refreshOnBlur": "",
                                "clearOnRefresh": false,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "console.log('docSection val '+JSON.stringify(data['docSection']) + \" string\" +(typeof data['docSection'] === 'string') + \" number \"+(typeof data['docSection'] === 'number'))",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "docSection",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [
                                    {
                                        "name": "EntityCodeAbsent",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "result = data['attributes'] === undefined || typeof data['attributes']['entityCode'] !== 'string' || data['attributes']['entityCode'].trim().length === 0"
                                        },
                                        "actions": [
                                            {
                                                "name": "EntityCodeAbsentAction",
                                                "type": "mergeComponentSchema",
                                                "schemaDefinition": "schema = {'data':{url:'',values:[]}}"
                                            }
                                        ]
                                    },
                                    {
                                        "name": "EntityCodePresent",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "result = data['attributes'] && typeof data['attributes']['entityCode'] === 'string' && data['attributes']['entityCode'].trim().length > 0"
                                        },
                                        "actions": [
                                            {
                                                "name": "EntityCodePresentAction",
                                                "type": "mergeComponentSchema",
                                                "schemaDefinition": "schema = {'data':{url:'https://form-service-ipb.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&entityCode={{data.attributes.entityCode}}&serviceKey=docSection'}}"
                                            }
                                        ]
                                    }
                                ],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "lazyLoad": false,
                                "selectValues": "data.DTS_FETCH_DOC_CODE",
                                "selectFields": "",
                                "disableLimit": true,
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 10000,
                                "authenticate": false,
                                "ignoreCache": false,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "elq2ms7",
                                "defaultValue": "",
                                "sort": ""
                            },
                            {
                                "label": "Document Code",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": true,
                                "autofocus": false,
                                "disabled": true,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "url",
                                "data": {
                                    "values": [
                                        {
                                            "label": "",
                                            "value": ""
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "headers": [
                                        {
                                            "key": "",
                                            "value": ""
                                        }
                                    ],
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "",
                                "valueProperty": "value",
                                "template": "<span>{{ item.label }} | {{item.value}}</span>",
                                "refreshOn": "docSection",
                                "refreshOnBlur": "",
                                "clearOnRefresh": true,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "if(typeof data['docVersion'] === 'object')\n  value = null",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "docCode",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [
                                    {
                                        "name": "Doc Section Empty Logic",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "result = typeof data['docSection'] !== 'string' || data['docSection'].trim().length ===0"
                                        },
                                        "actions": [
                                            {
                                                "name": "Doc Section Empty Action",
                                                "type": "mergeComponentSchema",
                                                "schemaDefinition": "schema = {'data':{url:'',values:[]}}"
                                            }
                                        ]
                                    },
                                    {
                                        "name": "Doc Section Present",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "result = typeof data['docSection'] === 'string' && data['docSection'].trim().length > 0"
                                        },
                                        "actions": [
                                            {
                                                "name": "Doc Section Present",
                                                "type": "mergeComponentSchema",
                                                "schemaDefinition": "schema = {'data':{url:'https://form-service-ipb.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&entityCode={{data.attributes.entityCode}}&activityId={{data.attributes.activityId}}&docSection={{data.docSection}}&serviceKey=docCode'}}"
                                            }
                                        ]
                                    }
                                ],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "lazyLoad": true,
                                "selectValues": "data.DTS_FETCH_DOC_CODE",
                                "selectFields": "",
                                "disableLimit": true,
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 10000,
                                "authenticate": false,
                                "ignoreCache": false,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "ee4vic8",
                                "defaultValue": "",
                                "sort": ""
                            },
                            {
                                "label": "Document Version",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "url",
                                "data": {
                                    "values": [
                                        {
                                            "label": "",
                                            "value": ""
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "headers": [
                                        {
                                            "key": "",
                                            "value": ""
                                        }
                                    ],
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "",
                                "valueProperty": "value",
                                "template": "<span>{{ item.label }}</span>",
                                "refreshOn": "docCode",
                                "refreshOnBlur": "",
                                "clearOnRefresh": true,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "docVersion",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [
                                    {
                                        "name": "Absent Logic",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "typeof data['docSection'] !== 'string' || data['docSection'].trim().length ===0 ||  typeof data['docCode'] !== 'string' || data['docCode'].trim().length ===0"
                                        },
                                        "actions": [
                                            {
                                                "name": "Empty Action",
                                                "type": "mergeComponentSchema",
                                                "schemaDefinition": "schema={'data':{'url':'','values':[]}}"
                                            }
                                        ]
                                    },
                                    {
                                        "name": "Present Logic",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "typeof data['docSection'] === 'string' && data['docSection'].trim().length > 0 && typeof data['docCode'] === 'string' && data['docCode'].trim().length > 0"
                                        },
                                        "actions": [
                                            {
                                                "name": "Present Action",
                                                "type": "mergeComponentSchema",
                                                "schemaDefinition": "schema = {'data':{url:'https://form-service-ipb.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&entityCode={{data.attributes.entityCode}}&docCode={{data.docCode}}&serviceKey=docVersion'}}"
                                            }
                                        ]
                                    }
                                ],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "lazyLoad": true,
                                "selectValues": "data.DTS_FETCH_DOC_VERSION",
                                "selectFields": "",
                                "disableLimit": true,
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 100,
                                "authenticate": false,
                                "ignoreCache": false,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "ezg0e8",
                                "defaultValue": "",
                                "sort": ""
                            },
                            {
                                "label": "Document Status",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "values",
                                "defaultValue": "Active",
                                "data": {
                                    "values": [
                                        {
                                            "label": "Superceded",
                                            "value": "Superceded"
                                        },
                                        {
                                            "label": "Cancelled",
                                            "value": "Cancelled"
                                        },
                                        {
                                            "label": "Deleted",
                                            "value": "Deleted"
                                        },
                                        {
                                            "label": "To Review",
                                            "value": "To Review"
                                        },
                                        {
                                            "label": "Active",
                                            "value": "Active"
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "id",
                                "valueProperty": "",
                                "template": "<span>{{ item.label }}</span>",
                                "refreshOn": "",
                                "refreshOnBlur": "",
                                "clearOnRefresh": false,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "if(value==undefined || data['docStatus']==undefined || value.trim().length ===0 || data['docStatus'].trim().length ===0) {\n  value = 'Active'\n}",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "docStatus",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "selectFields": "",
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 100,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "lazyLoad": true,
                                "authenticate": false,
                                "ignoreCache": false,
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "ea59nd"
                            },
                            {
                                "label": "Document Due Date",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "calendar",
                                    "altInput": true,
                                    "clickOpens": true,
                                    "enableDate": true,
                                    "mode": "single",
                                    "noCalendar": false,
                                    "format": "dd/MM/yyyy",
                                    "dateFormat": "dd/MM/yyyy",
                                    "useLocaleSettings": false,
                                    "saveAs": "text",
                                    "displayInTimezone": "viewer",
                                    "locale": "en"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "documentDueDate",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "eenzz4g",
                                "defaultValue": ""
                            },
                            {
                                "label": "Waive Request",
                                "labelPosition": "top",
                                "optionsLabelPosition": "right",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "inline": true,
                                "hidden": false,
                                "hideLabel": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": false,
                                "modalEdit": false,
                                "defaultValue": "No",
                                "values": [
                                    {
                                        "label": "Yes",
                                        "value": "W",
                                        "shortcut": ""
                                    },
                                    {
                                        "label": "No",
                                        "value": "No",
                                        "shortcut": ""
                                    }
                                ],
                                "dataType": "",
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "if(value!=='W' || data['waiveRequest']!=='W') {\n  value = 'No'\n}",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validate": {
                                    "required": false,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "errorLabel": "",
                                "errors": "",
                                "key": "waiveRequest",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "radio",
                                "input": true,
                                "placeholder": "",
                                "prefix": "",
                                "suffix": "",
                                "multiple": false,
                                "unique": false,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "widget": null,
                                "validateOn": "change",
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "inputType": "radio",
                                "fieldSet": false,
                                "id": "e91g1d"
                            },
                            {
                                "label": "Waiver Approval Date",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "calendar",
                                    "altInput": true,
                                    "clickOpens": true,
                                    "enableDate": true,
                                    "mode": "single",
                                    "noCalendar": false,
                                    "format": "dd/MM/yyyy",
                                    "dateFormat": "dd/MM/yyyy",
                                    "useLocaleSettings": false,
                                    "saveAs": "text",
                                    "displayInTimezone": "viewer",
                                    "locale": "en"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "waiverApprovalDate",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": true,
                                    "when": "waiveRequest",
                                    "eq": "W",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "eys27p",
                                "defaultValue": ""
                            },
                            {
                                "label": "Waive Until Date",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "calendar",
                                    "altInput": true,
                                    "clickOpens": true,
                                    "enableDate": true,
                                    "mode": "single",
                                    "noCalendar": false,
                                    "format": "dd/MM/yyyy",
                                    "dateFormat": "dd/MM/yyyy",
                                    "useLocaleSettings": false,
                                    "saveAs": "text",
                                    "displayInTimezone": "viewer",
                                    "locale": "en"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "waiveUntilDate",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": true,
                                    "when": "waiveRequest",
                                    "eq": "W",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "e03uq1",
                                "defaultValue": ""
                            },
                            {
                                "label": "Waiver Authorized By",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "input"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "waiverAuthorizedBy",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": true,
                                    "when": "waiveRequest",
                                    "eq": "W",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "e40uq5f",
                                "defaultValue": ""
                            },
                            {
                                "label": "Credit Use",
                                "labelPosition": "top",
                                "optionsLabelPosition": "right",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "inline": true,
                                "hidden": false,
                                "hideLabel": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": false,
                                "modalEdit": false,
                                "defaultValue": "No",
                                "values": [
                                    {
                                        "label": "Yes",
                                        "value": "Yes",
                                        "shortcut": ""
                                    },
                                    {
                                        "label": "No",
                                        "value": "No",
                                        "shortcut": ""
                                    }
                                ],
                                "dataType": "",
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "if(value!=='Yes' || data['creditUse']!=='Yes') {\n  value = 'No'\n}",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validate": {
                                    "required": false,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "errorLabel": "",
                                "errors": "",
                                "key": "creditUse",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [
                                    {
                                        "name": "ValueLogic",
                                        "trigger": {
                                            "type": "javascript",
                                            "javascript": "result=data['creditUse'] == undefined || data['creditUse'] == null || data['creditUse'].trim().length === 0"
                                        },
                                        "actions": [
                                            {
                                                "name": "ValueAction",
                                                "type": "value",
                                                "value": "value='No'"
                                            }
                                        ]
                                    }
                                ],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "radio",
                                "input": true,
                                "placeholder": "",
                                "prefix": "",
                                "suffix": "",
                                "multiple": false,
                                "unique": false,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "widget": null,
                                "validateOn": "change",
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "inputType": "radio",
                                "fieldSet": false,
                                "id": "e0ba0tn"
                            },
                            {
                                "label": "Credit Use Date",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "calendar",
                                    "altInput": true,
                                    "clickOpens": true,
                                    "enableDate": true,
                                    "mode": "single",
                                    "noCalendar": false,
                                    "format": "dd/MM/yyyy",
                                    "dateFormat": "dd/MM/yyyy",
                                    "useLocaleSettings": false,
                                    "saveAs": "text",
                                    "displayInTimezone": "viewer",
                                    "locale": "en"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "creditUseDate",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": "",
                                    "when": "",
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "etj1hv3",
                                "defaultValue": ""
                            },
                            {
                                "label": "Credit Approval Date",
                                "labelPosition": "top",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "prefix": "",
                                "suffix": "",
                                "widget": {
                                    "type": "calendar",
                                    "altInput": true,
                                    "clickOpens": true,
                                    "enableDate": true,
                                    "mode": "single",
                                    "noCalendar": false,
                                    "format": "dd/MM/yyyy",
                                    "dateFormat": "dd/MM/yyyy",
                                    "useLocaleSettings": false,
                                    "saveAs": "text",
                                    "displayInTimezone": "viewer",
                                    "locale": "en"
                                },
                                "inputMask": "",
                                "displayMask": "",
                                "allowMultipleMasks": false,
                                "customClass": "",
                                "tabindex": "",
                                "autocomplete": "",
                                "hidden": false,
                                "hideLabel": false,
                                "showWordCount": false,
                                "showCharCount": false,
                                "mask": false,
                                "autofocus": false,
                                "spellcheck": true,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "persistent": true,
                                "inputFormat": "plain",
                                "protected": false,
                                "dbIndex": false,
                                "case": "",
                                "truncateMultipleSpaces": false,
                                "encrypted": false,
                                "redrawOn": "",
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "pattern": "",
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "minLength": "",
                                    "maxLength": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "creditApprovalDate",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": "",
                                    "when": "",
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "textfield",
                                "input": true,
                                "refreshOn": "",
                                "dataGridLabel": false,
                                "addons": [],
                                "inputType": "text",
                                "id": "etdemt",
                                "defaultValue": ""
                            }
                        ],
                        "offset": 0,
                        "push": 0,
                        "pull": 0,
                        "size": "md",
                        "currentWidth": 5,
                        "width": 5
                    },
                    {
                        "components": [
                            {
                                "label": "Tracking Status",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "values",
                                "defaultValue": "Missing",
                                "data": {
                                    "values": [
                                        {
                                            "label": "Complete",
                                            "value": "Complete"
                                        },
                                        {
                                            "label": "Lux LDD - Missing",
                                            "value": "Lux LDD - Missing"
                                        },
                                        {
                                            "label": "Missing",
                                            "value": "Missing"
                                        },
                                        {
                                            "label": "Not required",
                                            "value": "Not required"
                                        },
                                        {
                                            "label": "Partially Accepted",
                                            "value": "Partially Accepted"
                                        },
                                        {
                                            "label": "Received but not reviewed",
                                            "value": "Received but not reviewed"
                                        },
                                        {
                                            "label": "Rejected",
                                            "value": "Rejected"
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "id",
                                "valueProperty": "",
                                "template": "<span>{{ item.label }}</span>",
                                "refreshOn": "",
                                "refreshOnBlur": "",
                                "clearOnRefresh": false,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": true,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "trackingStatus",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "selectFields": "",
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 100,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "lazyLoad": true,
                                "authenticate": false,
                                "ignoreCache": false,
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "eb02oja"
                            },
                            {
                                "label": "Physical Status",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "values",
                                "data": {
                                    "values": [
                                        {
                                            "label": "Copy",
                                            "value": "Copy"
                                        },
                                        {
                                            "label": "Copy - to be scanned",
                                            "value": "Copy - to be scanned"
                                        },
                                        {
                                            "label": "eDoc",
                                            "value": "eDoc"
                                        },
                                        {
                                            "label": "eDoc - to be scanned",
                                            "value": "eDoc - to be scanned"
                                        },
                                        {
                                            "label": "eSignedDoc",
                                            "value": "eSignedDoc"
                                        },
                                        {
                                            "label": "eSignedDoc - to be scanned",
                                            "value": "eSignedDoc - to be scanned"
                                        },
                                        {
                                            "label": "Fax",
                                            "value": "Fax"
                                        },
                                        {
                                            "label": "Fax - to be scanned",
                                            "value": "Fax - to be scanned"
                                        },
                                        {
                                            "label": "Not Applicable",
                                            "value": "Not Applicable"
                                        },
                                        {
                                            "label": "Original",
                                            "value": "Original"
                                        },
                                        {
                                            "label": "Original - to be scanned",
                                            "value": "Original - to be scanned"
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "id",
                                "valueProperty": "",
                                "template": "<span>{{ item.label }}</span>",
                                "refreshOn": "",
                                "refreshOnBlur": "",
                                "clearOnRefresh": false,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "physicalStatus",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "selectFields": "",
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 100,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "lazyLoad": true,
                                "authenticate": false,
                                "ignoreCache": false,
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "e43nz5",
                                "defaultValue": ""
                            },
                            {
                                "label": "Process Status",
                                "labelPosition": "top",
                                "widget": "choicesjs",
                                "placeholder": "",
                                "description": "",
                                "tooltip": "",
                                "customClass": "",
                                "tabindex": "",
                                "hidden": false,
                                "hideLabel": false,
                                "uniqueOptions": false,
                                "autofocus": false,
                                "disabled": false,
                                "tableView": true,
                                "modalEdit": false,
                                "multiple": false,
                                "dataSrc": "values",
                                "data": {
                                    "values": [
                                        {
                                            "label": "Awaiting Original",
                                            "value": "Awaiting Original"
                                        },
                                        {
                                            "label": "Critical (Credit)",
                                            "value": "Critical (Credit)"
                                        },
                                        {
                                            "label": "Facility Not currently Used",
                                            "value": "Facility Not currently Used"
                                        },
                                        {
                                            "label": "Internal Credit Document",
                                            "value": "Internal Credit Document"
                                        },
                                        {
                                            "label": "Migration",
                                            "value": "Migration"
                                        },
                                        {
                                            "label": "Not Yet Required",
                                            "value": "Not Yet Required"
                                        },
                                        {
                                            "label": "Pending Outside Council",
                                            "value": "Pending Outside Council"
                                        },
                                        {
                                            "label": "Redeemed",
                                            "value": "Redeemed"
                                        },
                                        {
                                            "label": "Re-doc Purpose Only",
                                            "value": "Re-doc Purpose Only"
                                        },
                                        {
                                            "label": "Registered",
                                            "value": "Registered"
                                        },
                                        {
                                            "label": "Returned to client",
                                            "value": "Returned to client"
                                        },
                                        {
                                            "label": "Sent for Registration",
                                            "value": "Sent for Registration"
                                        },
                                        {
                                            "label": "Sent For Scanning",
                                            "value": "Sent For Scanning"
                                        },
                                        {
                                            "label": "Sent to Client",
                                            "value": "Sent to Client"
                                        },
                                        {
                                            "label": "Sent to London",
                                            "value": "Sent to London"
                                        },
                                        {
                                            "label": "Sent to SG",
                                            "value": "Sent to SG"
                                        },
                                        {
                                            "label": "To be Registered",
                                            "value": "To be Registered"
                                        }
                                    ],
                                    "resource": "",
                                    "json": "",
                                    "url": "",
                                    "custom": ""
                                },
                                "dataType": "string",
                                "idPath": "id",
                                "valueProperty": "",
                                "template": "<span>{{ item.label }}</span>",
                                "refreshOn": "",
                                "refreshOnBlur": "",
                                "clearOnRefresh": false,
                                "searchEnabled": true,
                                "selectThreshold": 0.3,
                                "readOnlyValue": false,
                                "customOptions": {},
                                "useExactSearch": false,
                                "persistent": true,
                                "protected": false,
                                "dbIndex": false,
                                "encrypted": false,
                                "clearOnHide": true,
                                "customDefaultValue": "",
                                "calculateValue": "",
                                "calculateServer": false,
                                "allowCalculateOverride": false,
                                "validateOn": "change",
                                "validate": {
                                    "required": false,
                                    "onlyAvailableItems": false,
                                    "customMessage": "",
                                    "custom": "",
                                    "customPrivate": false,
                                    "json": "",
                                    "strictDateValidation": false,
                                    "multiple": false,
                                    "unique": false
                                },
                                "unique": false,
                                "errorLabel": "",
                                "errors": "",
                                "key": "processStatus",
                                "tags": [],
                                "properties": {},
                                "conditional": {
                                    "show": null,
                                    "when": null,
                                    "eq": "",
                                    "json": ""
                                },
                                "customConditional": "",
                                "logic": [],
                                "attributes": {},
                                "overlay": {
                                    "style": "",
                                    "page": "",
                                    "left": "",
                                    "top": "",
                                    "width": "",
                                    "height": ""
                                },
                                "type": "select",
                                "indexeddb": {
                                    "filter": {}
                                },
                                "selectFields": "",
                                "searchField": "",
                                "searchDebounce": 0.3,
                                "minSearch": 0,
                                "filter": "",
                                "limit": 100,
                                "redrawOn": "",
                                "input": true,
                                "prefix": "",
                                "suffix": "",
                                "dataGridLabel": false,
                                "showCharCount": false,
                                "showWordCount": false,
                                "allowMultipleMasks": false,
                                "addons": [],
                                "lazyLoad": true,
                                "authenticate": false,
                                "ignoreCache": false,
                                "fuseOptions": {
                                    "include": "score",
                                    "threshold": 0.3
                                },
                                "id": "eszzh8",
                                "defaultValue": ""
                            }
                        ],
                        "offset": 0,
                        "push": 0,
                        "pull": 0,
                        "size": "md",
                        "currentWidth": 5,
                        "width": 5
                    }
                ],
                "autoAdjust": false,
                "customClass": "",
                "hidden": false,
                "hideLabel": false,
                "modalEdit": false,
                "key": "columns",
                "tags": [],
                "properties": {},
                "conditional": {
                    "show": null,
                    "when": null,
                    "eq": "",
                    "json": ""
                },
                "customConditional": "",
                "logic": [],
                "attributes": {},
                "overlay": {
                    "style": "",
                    "page": "",
                    "left": "",
                    "top": "",
                    "width": "",
                    "height": ""
                },
                "type": "columns",
                "input": false,
                "tableView": false,
                "placeholder": "",
                "prefix": "",
                "suffix": "",
                "multiple": false,
                "defaultValue": null,
                "protected": false,
                "unique": false,
                "persistent": false,
                "clearOnHide": false,
                "refreshOn": "",
                "redrawOn": "",
                "dataGridLabel": false,
                "labelPosition": "top",
                "description": "",
                "errorLabel": "",
                "tooltip": "",
                "tabindex": "",
                "disabled": false,
                "autofocus": false,
                "dbIndex": false,
                "customDefaultValue": "",
                "calculateValue": "",
                "calculateServer": false,
                "widget": null,
                "validateOn": "change",
                "validate": {
                    "required": false,
                    "custom": "",
                    "customPrivate": false,
                    "strictDateValidation": false,
                    "multiple": false,
                    "unique": false
                },
                "allowCalculateOverride": false,
                "encrypted": false,
                "showCharCount": false,
                "showWordCount": false,
                "allowMultipleMasks": false,
                "addons": [],
                "tree": false,
                "lazyLoad": false,
                "id": "ewa6fas"
            }
        ]
    },
    "actionSchema": {
        "components": [
            {
                "label": "Abandon",
                "action": "custom",
                "showValidations": false,
                "theme": "danger",
                "size": "md",
                "block": false,
                "leftIcon": "",
                "rightIcon": "",
                "shortcut": "",
                "description": "",
                "tooltip": "",
                "customClass": "right",
                "tabindex": "",
                "disableOnInvalid": false,
                "hidden": false,
                "autofocus": false,
                "disabled": false,
                "tableView": false,
                "modalEdit": false,
                "key": "defAbandonFbf4B04E65Cd45BaB4B9F8Be2Ad28105",
                "tags": [
                    "defaultAbandon"
                ],
                "properties": {},
                "conditional": {
                    "show": null,
                    "when": null,
                    "eq": "",
                    "json": ""
                },
                "customConditional": "",
                "logic": [],
                "attributes": {},
                "overlay": {
                    "style": "",
                    "page": "",
                    "left": "",
                    "top": "",
                    "width": "",
                    "height": ""
                },
                "type": "button",
                "custom": "const postSubmitActionMapping ={\n    confirmation:{\n\t  needConfirmation:true,\n\t  title:'Are you sure you want to abandon this ticket?',\n\t  confirmText:'Confirm'\n\t},\n    postSubmitConfirmation:{\n\t     confirmationMessage: 'Ticket Abandoned Successfully',\n\t     closeWindow:true\n\t}\n}\n\ndata['postSubmitActionMapping'] = postSubmitActionMapping\n\ndata['COMPONENT_KEY'] = component['key'];\n\n\ndata['docStatus'] = 'Cancelled'\n\ninstance.root.executeSubmit();",
                "input": true,
                "placeholder": "",
                "prefix": "",
                "suffix": "",
                "multiple": false,
                "defaultValue": null,
                "protected": false,
                "unique": false,
                "persistent": false,
                "clearOnHide": true,
                "refreshOn": "",
                "redrawOn": "",
                "dataGridLabel": true,
                "labelPosition": "top",
                "errorLabel": "",
                "hideLabel": false,
                "dbIndex": false,
                "customDefaultValue": "",
                "calculateValue": "",
                "calculateServer": false,
                "widget": {
                    "type": "input"
                },
                "validateOn": "change",
                "validate": {
                    "required": false,
                    "custom": "",
                    "customPrivate": false,
                    "strictDateValidation": false,
                    "multiple": false,
                    "unique": false
                },
                "allowCalculateOverride": false,
                "encrypted": false,
                "showCharCount": false,
                "showWordCount": false,
                "allowMultipleMasks": false,
                "addons": [],
                "id": "ecrpkc"
            },
            {
                "label": "Submit",
                "action": "custom",
                "showValidations": false,
                "theme": "primary",
                "size": "md",
                "block": false,
                "leftIcon": "",
                "rightIcon": "",
                "shortcut": "",
                "description": "",
                "tooltip": "",
                "customClass": "",
                "tabindex": "",
                "disableOnInvalid": true,
                "hidden": false,
                "autofocus": false,
                "disabled": false,
                "tableView": false,
                "modalEdit": false,
                "key": "workflowButton_activity_1ncdena",
                "tags": [
                    "workflowAction"
                ],
                "properties": {},
                "conditional": {
                    "show": null,
                    "when": null,
                    "eq": "",
                    "json": ""
                },
                "customConditional": "",
                "logic": [],
                "attributes": {},
                "overlay": {
                    "style": "",
                    "page": "",
                    "left": "",
                    "top": "",
                    "width": "",
                    "height": ""
                },
                "type": "button",
                "custom": "const workflowActionMapping = {};\nconst postSubmitActionMapping ={\n    postSubmitConfirmation:{\n\t     confirmationMessage: 'Data Submitted Successfully',\n\t     closeWindow:true\n\t}\n}\nObject.entries(component.properties).forEach((entry) => {\n  const [key, value] = entry;\n  workflowActionMapping[key] = value;\n});\ndata['workflowActionMapping'] = workflowActionMapping;\ndata['postSubmitActionMapping'] = postSubmitActionMapping\n\ndata['COMPONENT_KEY'] = component['key'];\n\ninstance.root.executeSubmit();",
                "input": true,
                "placeholder": "",
                "prefix": "",
                "suffix": "",
                "multiple": false,
                "defaultValue": null,
                "protected": false,
                "unique": false,
                "persistent": false,
                "clearOnHide": true,
                "refreshOn": "",
                "redrawOn": "",
                "dataGridLabel": true,
                "labelPosition": "top",
                "errorLabel": "",
                "hideLabel": false,
                "dbIndex": false,
                "customDefaultValue": "",
                "calculateValue": "",
                "calculateServer": false,
                "widget": {
                    "type": "input"
                },
                "validateOn": "change",
                "validate": {
                    "required": false,
                    "custom": "",
                    "customPrivate": false,
                    "strictDateValidation": false,
                    "multiple": false,
                    "unique": false
                },
                "allowCalculateOverride": false,
                "encrypted": false,
                "showCharCount": false,
                "showWordCount": false,
                "allowMultipleMasks": false,
                "addons": [],
                "id": "edt1ql7"
            }
        ]
    },
    "formData": {
        "processStatus": "",
        "pid": "DJR969P",
        "docCodeLabel": "Passport for Account Holders",
        "waiverApprovalDate": "10/05/2024",
        "docSection": 1,
        "physicalStatus": "",
        "docVersion": "",
        "documentDueDate": "",
        "waiveRequest": "W",
        "lastCommentTs": 1716542751245,
        "docCode": "040",
        "creditUseDate": "",
        "waiverAuthorizedBy": "Mistry",
        "docId": 2990,
        "docStatus": "Active",
        "primusPartyId": 90728,
        "workflowButton_activity_1hf0srq": true,
        "defAbandonFbf4B04E65Cd45BaB4B9F8Be2Ad28105": false,
        "creditApprovalDate": "",
        "workflowButton_activity_1ncdena": true,
        "docSectionLabel": "Account Opening",
        "waiveUntilDate": "31/05/2024",
        "defAbandon42A91B0C7Efc401BB1C76Cd84038B7B4": false,
        "creditUse": "No",
        "trackingStatus": "Missing",
        "attributes": {
            "pageFrom": "ITunes",
            "caseId": "86000011046",
            "sugarCaseId": "",
            "eci": "0653546489",
            "accountNumber": "3041450",
            "businessSystemCode": "OFR",
            "initiatorName": "",
            "initiatorSid": "N668956",
            "initiatingTeamName": "WM Capital Advisor International",
            "initiatingTeamCode": "WM_CAP_ADVSR_INTL",
            "hierarchyId": "28159",
            "categoryCode": "ACT_MNT",
            "categoryDesc": "Account Maintenance",
            "requestTypeCode": "CRDT_DOC_UPLD",
            "requestTypeDesc": "Credit Documentation - Upload",
            "requestSubTypeCode": "25016_NA",
            "requestSubTypeDesc": "NA",
            "entityCode": "FRA",
            "activeEnvironment": "",
            "activePlatform": "",
            "bankCode": "",
            "gwmIdentifier": "I0000588432",
            "largeClient": "",
            "loggedInUserSid": "N668956",
            "caseDetails": "undefined",
            "corporateProductCode": "SD",
            "initiatedBy": "ACCT_INIT",
            "source": "InitiateRequest",
            "spn": "2376036",
            "viewTypeCd": "ACCT_INIT",
            "env": "local",
            "gwmId": "I0000588432",
            "activityId": "8be82409-1996-11ef-8ff8-06d8fafc6051",
            "activityTypeCode": "Activity_1ncdena",
            "activityDisplayName": "Update Document Details",
            "taskStartDate": "24 May 2024 11:56 AM",
            "taskDueDate": null,
            "processId": "6aaf80ed-1996-11ef-ab2e-02384f203301",
            "processStatus": "New",
            "assigneeName": "Bhavini Mistry",
            "assigneeSid": "V130687",
            "ownerName": "Bhavini Mistry",
            "ownerSid": "V130687",
            "owningTeamCode": "act_admin_emea",
            "owningTeamName": "ACT Admin EMEA",
            "processDefinitionId": "documentTracker",
            "processDefinitionVersion": "46",
            "formId": "documentTracker-46-Activity_1ncdena-WORKFLOW"
        }
    }
}



nabanita


{
    "traceId": "1abb3f1b332d446e7d07a79de4f5ad2b",
    "message": "Success",
    "config": {
        "bodySchema": "{\"display\":\"form\",\"components\":[{\"key\":\"fieldSet8\",\"type\":\"fieldset\",\"label\":\"Field Set\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Individual or Entity?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"defaultValue\":\"individual\",\"values\":[{\"label\":\"Individual\",\"value\":\"individual\",\"shortcut\":\"\"},{\"label\":\"Entity\",\"value\":\"entity\",\"shortcut\":\"\"}],\"clearOnHide\":false,\"validate\":{\"required\":true},\"key\":\"individualOrEntity\",\"logic\":[{\"name\":\"onIndividualOrEntityChange\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"// Check if the previous value is already stored\\r\\nif (typeof instance.prevValue === 'individualOrEntity') {\\r\\n  // Initialize the previous value with the current value\\r\\n  instance.prevValue = data['individualOrEntity'];\\r\\n  return true;\\r\\n}\\r\\n\\r\\n// Check if the value has changed\\r\\nif (instance.prevValue !== data['individualOrEntity']) {\\r\\n  // Update the previous value with the current value\\r\\n  instance.prevValue = data['individualOrEntity'];\\r\\n  return true;\\r\\n}\\r\\nreturn false;\"},\"actions\":[{\"name\":\"onChange\",\"type\":\"customAction\",\"customAction\":\"\\r\\n\\r\\n  var tabs = document.querySelectorAll('[ref=\\\"tabLink-tabs\\\"]')\\r\\n  var tabPanels = document.querySelectorAll('[ref=\\\"tab-tabs\\\"]')\\r\\n  tabPanels.forEach(pane=> {pane.style.display=\\\"none\\\";\\r\\n    pane.classList.remove('active','show')});\\r\\n  tabs.forEach(link => link.classList.remove('active'));\\r\\n  if(value === 'entity'){\\r\\n    entityInformation = tabs[0]\\r\\n    entityInformation.style.display=\\\"\\\";\\r\\n    entityInformation.classList.add('active')\\r\\n    tabPanels[0].classList.add('active','show')\\r\\n    tabPanels[0].style.display=\\\"block\\\";\\r\\n    \\r\\n  }else{\\r\\n    entityInformation = tabs[0];\\r\\n   \\r\\n    tabs[1].style.display=\\\"block\\\";\\r\\n    entityInformation.style.display=\\\"none\\\";\\r\\n    tabs[1].classList.add('active')\\r\\n    tabPanels[1].classList.add('active','show')\\r\\n    tabPanels[1].style.display=\\\"block\\\";\\r\\n    tabPanels[0].style.display=\\\"none\\\";\\r\\n  }\\r\\n\\r\\n\\r\\n\"}]}],\"type\":\"radio\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns8\",\"type\":\"columns\",\"input\":false,\"tableView\":false}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"key\":\"columns11\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"key\":\"fieldSet1\",\"type\":\"fieldset\",\"label\":\"Field Set\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Reason for KYC request\",\"widget\":\"choicesjs\",\"description\":\"Please select the reason for a KYC request to be raised\",\"tableView\":true,\"data\":{\"values\":[{\"label\":\"Retitle\",\"value\":\"retitle\"},{\"label\":\"Mortgage/Credit\",\"value\":\"mortgageCredit\"},{\"label\":\"LOB transfers (that do not qualify for LOB exception)\",\"value\":\"lobTransfers\"},{\"label\":\"DAF\",\"value\":\"daf\"},{\"label\":\"529\",\"value\":\"529\"},{\"label\":\"CD\",\"value\":\"cd\"},{\"label\":\"Medallion Stamp\",\"value\":\"medallionStamp\"},{\"label\":\"Life Insurance\",\"value\":\"lifeInsurance\"},{\"label\":\"Credit Card\",\"value\":\"creditCard\"},{\"label\":\"Client Controller\",\"value\":\"clientController\"},{\"label\":\"Account Controller\",\"value\":\"accountController\"},{\"label\":\"Grantor\",\"value\":\"grantor\"},{\"label\":\"Trustee\",\"value\":\"trustee\"},{\"label\":\"POA\",\"value\":\"poa\"},{\"label\":\"Inquiry Only\",\"value\":\"inquiryOnly\"},{\"label\":\"Screening only\",\"value\":\"screeningOnly\"},{\"label\":\"Sub-user\",\"value\":\"subUser\"},{\"label\":\"AO-related request\",\"value\":\"aoRelatedRequest\"},{\"label\":\"Onboarding for future accounts\",\"value\":\"onboardingForFutureAccounts\"}]},\"validate\":{\"required\":true},\"key\":\"reasonForKycRequest\",\"type\":\"select\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns32\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Tabs\",\"components\":[{\"label\":\"Entity Information\",\"key\":\"entityInformation\",\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Customer Entity Type\",\"labelPosition\":\"left-left\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"defaultValue\":\"noah\",\"data\":{\"values\":[{\"label\":\"Non Operating/Asset Holding Entities\",\"value\":\"noah\"},{\"label\":\"Organizations\",\"value\":\"organizations\"},{\"label\":\"Operating Company\",\"value\":\"operatingCompany\"},{\"label\":\"Financial Institution, or in Financial Services Industry\",\"value\":\"nbfi\"}]},\"validate\":{\"required\":true},\"key\":\"customerEntityType\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"type\":\"select\",\"input\":true}],\"width\":10,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":10},{\"components\":[],\"width\":2,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":2}],\"key\":\"columns9\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"key\":\"fieldSet\",\"type\":\"fieldset\",\"label\":\"Field Set\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Is the entity organized as a not for profit?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"nonProfit\",\"conditional\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"organizations\"},\"type\":\"radio\",\"input\":true}]},{\"hidden\":true,\"key\":\"fieldSet17\",\"conditional\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"noah\"},\"type\":\"fieldset\",\"label\":\"Field Set\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Is the client a Trust?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isTrust\",\"type\":\"radio\",\"input\":true},{\"label\":\"Is the client engaged in holding the securities of (or other equity interests in) companies and enterprises for the purpose of owning a controlling interest or influencing the management decisions of these firms?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"holdingSecurities\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"no\"},\"type\":\"radio\",\"input\":true},{\"label\":\"Is the client engaged in offering financial services, which include: broker dealers, fund managers, investment advisors, mutual funds, or commodity traders?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"offersFinSvc\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"no\"},\"type\":\"radio\",\"input\":true},{\"label\":\"Is the client entity established to conduct commercial activities that will provide its customers with either products (goods) or services?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isCommercial\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"no\"},\"type\":\"radio\",\"input\":true},{\"label\":\"Does the client have capital that is limited to the assets of a single individual/family or multiple related individuals for the purpose of investment of personal assets?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isPIC\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"no\"},\"type\":\"radio\",\"input\":true},{\"label\":\"Is the client a charitable trust that awards grants to charities?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isCharitable\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"yes\"},\"type\":\"radio\",\"input\":true}]},{\"hidden\":true,\"key\":\"fieldSet18\",\"conditional\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"operatingCompany\"},\"type\":\"fieldset\",\"label\":\"Field Set\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Is the entity publicly traded?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isPublic\",\"type\":\"radio\",\"input\":true},{\"label\":\"Revenue?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"< 25 million USD\",\"value\":\"lessThan\",\"shortcut\":\"\"},{\"label\":\"> 25 million USD\",\"value\":\"greaterThan\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isRevenue25\",\"type\":\"radio\",\"input\":true}]}],\"width\":12,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":12},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns10\",\"type\":\"columns\",\"input\":false,\"tableView\":false}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"key\":\"columns13\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"title\":\"NAICS Code Checklist\",\"customClass\":\"noBorderPanel\",\"collapsible\":false,\"key\":\"naicChecklist\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"customConditional\":\"show = data.customerEntityType? data.customerEntityType.length>0: false\",\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Choose NAIC code\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"naicCode\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"logic\":[{\"name\":\"noah\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"noah\"}},\"actions\":[{\"name\":\"noah\",\"type\":\"property\",\"property\":{\"label\":\"Label\",\"value\":\"label\",\"type\":\"string\"},\"text\":\"Choose NAIC code for Client Type: Non-Operating/Asset Holding Entities\"}]},{\"name\":\"organizations\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"organizations\"}},\"actions\":[{\"name\":\"organizations\",\"type\":\"property\",\"property\":{\"label\":\"Label\",\"value\":\"label\",\"type\":\"string\"},\"text\":\"Choose NAIC code for Client Type: Organizations\"}]},{\"name\":\"nbfi\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"nbfi\"}},\"actions\":[]},{\"name\":\"operatingCompany less\",\"trigger\":{\"type\":\"javascript\",\"simple\":{},\"javascript\":\"result = (data.isPublic == 'no') & (data.isRevenue25 == 'lessThan')\"},\"actions\":[{\"name\":\"lessThan\",\"type\":\"property\",\"property\":{\"label\":\"Label\",\"value\":\"label\",\"type\":\"string\"},\"text\":\"Choose NAIC code for Client Type: Small Private Operating Companies (Revenues < $25MM)\"}]},{\"name\":\"operatingCompany greater\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = (data.isPublic == 'no') & (data.isRevenue25 == 'greaterThan')\"},\"actions\":[{\"name\":\"greater\",\"type\":\"property\",\"property\":{\"label\":\"Label\",\"value\":\"label\",\"type\":\"string\"},\"text\":\"Choose NAIC code for Client Type: Large Private Operating Companies (Revenues > $25MM)\"}]},{\"name\":\"opCo Public\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"isPublic\",\"eq\":\"yes\"}},\"actions\":[{\"name\":\"public\",\"type\":\"property\",\"property\":{\"label\":\"Label\",\"value\":\"label\",\"type\":\"string\"},\"text\":\"Choose NAIC code for Client Type: Public Operating Companies\"}]},{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 1\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=naicCode'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"naicChecklist\"},{\"label\":\"Entity Name\",\"widget\":\"choicesjs\",\"description\":\"Key words within the entity name include, but are not limited to: “Fund”, “holdings”, “distribution”, “trust”\",\"tableView\":true,\"data\":{\"values\":[{\"label\":\"Fund\",\"value\":\"fund\"},{\"label\":\"Holding\",\"value\":\"holding\"},{\"label\":\"Distribution\",\"value\":\"distribution\"},{\"label\":\"Trust\",\"value\":\"trust\"},{\"label\":\"Operating\",\"value\":\"operating\"},{\"label\":\"None of the Above\",\"value\":\"noneOfTheAbove\"},{\"label\":\"Other\",\"value\":\"other\"}]},\"validate\":{\"required\":true},\"key\":\"entityName\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"naicChecklist\"}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"key\":\"columns14\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Is the Entity Type (Legal Entity Structure) one of these Professional Limited Liability Company or Corporation or Sole Proprietorship or General Partnership?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"isCorp\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"naicChecklist\"},{\"label\":\"Does the entity have any intermediary owners (including owners with less than 10% equity ownership) that are a fund or operating company?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"intermediaryOwners\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"naicChecklist\"}],\"width\":12,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":12},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns16\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Online Search (Select all that apply)\",\"optionsLabelPosition\":\"bottom\",\"tableView\":false,\"defaultValue\":{\"companyWebsite\":false,\"significantOnlinePresence\":false,\"registrationWithRegulator\":false,\"noneOfTheAboveOther\":false},\"values\":[{\"label\":\"Company website\",\"value\":\"companyWebsite\",\"shortcut\":\"\"},{\"label\":\"Significant online presence\",\"value\":\"significantOnlinePresence\",\"shortcut\":\"\"},{\"label\":\"Registration with Regulator\",\"value\":\"registrationWithRegulator\",\"shortcut\":\"\"},{\"label\":\"None of the Above - Other\",\"value\":\"noneOfTheAboveOther\",\"shortcut\":\"\"}],\"key\":\"onlineSearch\",\"type\":\"selectboxes\",\"input\":true,\"inputType\":\"checkbox\",\"parentPanelKey\":\"naicChecklist\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[{\"label\":\"Detailed nature and purpose of entity: Does the client?\",\"optionsLabelPosition\":\"bottom\",\"tableView\":false,\"defaultValue\":{\"haveEmployeesPayroll\":false,\"generateRevenue\":false,\"receiveRentalIncome\":false,\"provideAGoodOrService\":false,\"acceptThirdPartyMoney\":false,\"noneOfTheAbove\":false,\"other\":false},\"values\":[{\"label\":\"Have employees/payroll\",\"value\":\"haveEmployeesPayroll\",\"shortcut\":\"\"},{\"label\":\"Generate revenue\",\"value\":\"generateRevenue\",\"shortcut\":\"\"},{\"label\":\"Receive rental income\",\"value\":\"receiveRentalIncome\",\"shortcut\":\"\"},{\"label\":\"Provide a good or service\",\"value\":\"provideAGoodOrService\",\"shortcut\":\"\"},{\"label\":\"Accept third party money\",\"value\":\"acceptThirdPartyMoney\",\"shortcut\":\"\"},{\"label\":\"None of the Above\",\"value\":\"noneOfTheAbove\",\"shortcut\":\"\"},{\"label\":\"Other\",\"value\":\"other\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"detailedNature\",\"type\":\"selectboxes\",\"input\":true,\"inputType\":\"checkbox\",\"parentPanelKey\":\"naicChecklist\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns18\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Synopsis of Results/Findings\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"synopsisOfResults\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"naicChecklist\"}],\"width\":12,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":12},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns15\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"key\":\"columns17\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"Client Core Information\",\"key\":\"clientCoreInformation\",\"components\":[{\"title\":\"Personal\",\"collapsible\":false,\"key\":\"personal\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"First Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"firstName\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"personal\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Middle Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"middleName\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"personal\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Last Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"lastName\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"personal\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Generation\",\"widget\":\"choicesjs\",\"tableView\":true,\"data\":{\"values\":[{\"label\":\"I/First\",\"value\":\"first\"},{\"label\":\"II/Second\",\"value\":\"second\"},{\"label\":\"III/Third\",\"value\":\"third\"},{\"label\":\"IV/Fourth\",\"value\":\"fourth\"},{\"label\":\"Jr.\",\"value\":\"jr\"},{\"label\":\"Sr.\",\"value\":\"sr\"}]},\"key\":\"generation\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"personal\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hidden\":true,\"key\":\"columns2\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"Entity\",\"collapsible\":false,\"key\":\"entity\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Client's Full Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"clientFullName\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"entity\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Legal Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"legalName\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"entity\"},{\"label\":\"Legal Entity Structure\",\"widget\":\"choicesjs\",\"tableView\":true,\"data\":{\"values\":[{\"label\":\"Corporation\",\"value\":\"corporation\"},{\"label\":\"C Corporation\",\"value\":\"cCorporation\"},{\"label\":\"Educational Organization\",\"value\":\"educationalOrganization\"},{\"label\":\"Estate\",\"value\":\"estate\"},{\"label\":\"Financial Institution\",\"value\":\"financialInstitution\"},{\"label\":\"Funds and Plans\",\"value\":\"fundsAndPlans\"},{\"label\":\"General Partnership\",\"value\":\"generalPartnership\"},{\"label\":\"Governmental Entity - Central Bank\",\"value\":\"governmentalEntityCentralBank\"},{\"label\":\"Governmental Entity - Central Government\",\"value\":\"governmentalEntityCentralGovernment\"},{\"label\":\"Governmental Entity - Central Government Agency\",\"value\":\"governmentalEntityCentralGovernmentAgency\"},{\"label\":\"Governmental Entity - Central Government Sponsored Agency\",\"value\":\"governmentalEntityCentralGovernmentSponsoredAgency\"},{\"label\":\"Governmental Entity - Public State Province - General Obligation\",\"value\":\"governmentalEntityPublicStateProvinceGeneralObligation\"},{\"label\":\"Governmental Entity - Public State Province - Private Repayment\",\"value\":\"governmentalEntityPublicStateProvincePrivateRepayment\"},{\"label\":\"Governmental Entity - Public State Province - Special Purpose\",\"value\":\"governmentalEntityPublicStateProvinceSpecialPurpose\"},{\"label\":\"Governmental Entity - Quasi-Governmental Body\",\"value\":\"governmentalEntityQuasiGovernmentalBody\"},{\"label\":\"Governmental Entity - US Government Sponsored Agency\",\"value\":\"governmentalEntityUsGovernmentSponsoredAgency\"},{\"label\":\"Guardianship Conservatorship\",\"value\":\"guardianshipConservatorship\"},{\"label\":\"Limited Liability Corporation\",\"value\":\"limitedLiabilityCorporation\"},{\"label\":\"Limited Liability Partnership\",\"value\":\"limitedLiabilityPartnership\"},{\"label\":\"Limited Partnership\",\"value\":\"limitedPartnership\"},{\"label\":\"Manager Managed LLC\",\"value\":\"managerManagedLlc\"},{\"label\":\"Member Managed LLC\",\"value\":\"memberManagedLlc\"},{\"label\":\"Non-Profit Organization\",\"value\":\"nonProfitOrganization\"},{\"label\":\"Partnership Joint Venture\",\"value\":\"partnershipJointVenture\"},{\"label\":\"Public City/Municipality\",\"value\":\"publicCityMunicipality\"},{\"label\":\"Public County/Parish\",\"value\":\"publicCountyParish\"},{\"label\":\"Public Federal\",\"value\":\"publicFederal\"},{\"label\":\"Public School District\",\"value\":\"publicSchoolDistrict\"},{\"label\":\"S Corporation\",\"value\":\"sCorporation\"},{\"label\":\"Sole Proprietorship\",\"value\":\"soleProprietorship\"},{\"label\":\"Special Purpose Entity\",\"value\":\"specialPurposeEntity\"},{\"label\":\"Supranational\",\"value\":\"supranational\"},{\"label\":\"Trust\",\"value\":\"trust\"},{\"label\":\"Unincorporated Business Association/Organization\",\"value\":\"unincorporatedBusinessAssociationOrganization\"}]},\"validate\":{\"required\":true},\"key\":\"legalEntityStructure\",\"logic\":[{\"name\":\"Trust\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"isTheClientATrust\",\"eq\":\"yes\"}},\"actions\":[{\"name\":\"Trust\",\"type\":\"value\",\"value\":\"value = \\\"trust\\\"\"}]}],\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"entity\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Doing Business As (aka. DBA) name(s)\",\"applyMaskOn\":\"change\",\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"doingBusinessAs\",\"conditional\":{\"show\":true,\"when\":\"solePropDBA\",\"eq\":\"yes\"},\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"entity\"},{\"label\":\"Date of Organization\",\"format\":\"yyyy-MM-dd\",\"tableView\":false,\"datePicker\":{\"disableWeekends\":false,\"disableWeekdays\":false},\"enableTime\":false,\"validate\":{\"required\":true},\"enableMinDateInput\":false,\"enableMaxDateInput\":false,\"key\":\"dateOfOrganization\",\"type\":\"datetime\",\"input\":true,\"widget\":{\"type\":\"calendar\",\"displayInTimezone\":\"viewer\",\"locale\":\"en\",\"useLocaleSettings\":false,\"allowInput\":true,\"mode\":\"single\",\"enableTime\":false,\"noCalendar\":false,\"format\":\"yyyy-MM-dd\",\"hourIncrement\":1,\"minuteIncrement\":1,\"time_24hr\":false,\"minDate\":null,\"disableWeekends\":false,\"disableWeekdays\":false,\"maxDate\":null},\"parentPanelKey\":\"entity\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Does the Sole Propietorship have DBA Name(s)?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"solePropDBA\",\"conditional\":{\"show\":true,\"when\":\"legalEntityStructure\",\"eq\":\"solePropietorship\"},\"customConditional\":\"show = (data.legalEntityStructure = 'solePropietorship' + data.customerEntityType = 'operatingCompany')\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"entity\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"key\":\"columns1\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"Address\",\"collapsible\":false,\"key\":\"address\",\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Address Line 1\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"addressLine1\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"address\"},{\"label\":\"Address Line 2\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"addressLine2\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"address\"},{\"label\":\"Address Line 3\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"addressLine3\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"address\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[{\"label\":\"City\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"city\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"address\"},{\"label\":\"State\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"label\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"state\",\"conditional\":{\"show\":true,\"when\":\"country\",\"eq\":\"United States Of America\"},\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=state'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"address\"},{\"label\":\"Country\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"country\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=country'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"address\"},{\"label\":\"Postal Code\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true,\"customMessage\":\"Please enter a valid postal code\"},\"key\":\"postalCode\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"address\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Address used for CIP?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"defaultValue\":\"yes\",\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"addressUsedForCip\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"address\"}],\"size\":\"md\",\"currentWidth\":3,\"width\":3}],\"key\":\"columns7\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"Government ID\",\"collapsible\":false,\"key\":\"governmentId\",\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Primary country of citizenship\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryCitizenship\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryCitizenship'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"},{\"label\":\"Country of Organization\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryOrganization\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryOrganization'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"},{\"label\":\"State of Organization\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"stateOrganization\",\"conditional\":{\"show\":true,\"when\":\"countryOrganization\",\"eq\":\"United States Of America\"},\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=stateOrganization'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Primary country of assets\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryAssets\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryAssets'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Form of Government ID\",\"widget\":\"choicesjs\",\"tableView\":true,\"data\":{\"values\":[{\"label\":\"Social Security Number\",\"value\":\"socialSecurityNumber\"},{\"label\":\"TIN\",\"value\":\"tin\"}]},\"validate\":{\"required\":true},\"key\":\"formOfId\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"governmentId\"},{\"label\":\"ID Number\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"idNumber\",\"logic\":[{\"name\":\"Mask\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"formOfId\",\"eq\":\"socialSecurityNumber\"}},\"actions\":[{\"name\":\"SSN\",\"type\":\"property\",\"property\":{\"label\":\"Input Mask\",\"value\":\"inputMask\",\"type\":\"string\"},\"text\":\"999-99-9999\"}]},{\"name\":\"TIN Mask\",\"trigger\":{\"type\":\"simple\",\"simple\":{\"show\":true,\"when\":\"formOfGovernmentId\",\"eq\":\"tin\"}},\"actions\":[{\"name\":\"TIN Mask\",\"type\":\"property\",\"property\":{\"label\":\"Input Mask\",\"value\":\"inputMask\",\"type\":\"string\"},\"text\":\"99-9999999\"}]}],\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"governmentId\"},{\"label\":\"Issuing Authority\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"refreshOn\":\"data\",\"refreshOnBlur\":\"countryCitizenship\",\"customDefaultValue\":\"value = data.countryCitizenship\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"issuingAuthority\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=issuingAuthority'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"},{\"label\":\"Date of Birth\",\"format\":\"yyyy-MM-dd\",\"hidden\":true,\"tableView\":false,\"datePicker\":{\"disableWeekends\":false,\"disableWeekdays\":false},\"enableTime\":false,\"validate\":{\"required\":true},\"enableMinDateInput\":false,\"enableMaxDateInput\":false,\"key\":\"dob\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"datetime\",\"input\":true,\"widget\":{\"type\":\"calendar\",\"displayInTimezone\":\"viewer\",\"locale\":\"en\",\"useLocaleSettings\":false,\"allowInput\":true,\"mode\":\"single\",\"enableTime\":false,\"noCalendar\":false,\"format\":\"yyyy-MM-dd\",\"hourIncrement\":1,\"minuteIncrement\":1,\"time_24hr\":false,\"minDate\":null,\"disableWeekends\":false,\"disableWeekdays\":false,\"maxDate\":null},\"parentPanelKey\":\"governmentId\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Primary country of domicile\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryDomicile\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryDomicile'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"},{\"label\":\"Primary state of domicile\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"stateDomicile\",\"conditional\":{\"show\":true,\"when\":\"countryDomicile\",\"eq\":\"United States Of America\"},\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=stateDomicile'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"governmentId\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"key\":\"columns3\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"Employment Info\",\"collapsible\":false,\"key\":\"employmentInfo\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Employment Status\",\"optionsLabelPosition\":\"bottom\",\"tableView\":false,\"defaultValue\":{\"employed\":false,\"former\":false,\"other\":false,\"retired\":false,\"student\":false,\"unemployed\":false,\"selfEmployed\":false},\"values\":[{\"label\":\"Employed\",\"value\":\"employed\",\"shortcut\":\"\"},{\"label\":\"Former\",\"value\":\"former\",\"shortcut\":\"\"},{\"label\":\"Other\",\"value\":\"other\",\"shortcut\":\"\"},{\"label\":\"Retired\",\"value\":\"retired\",\"shortcut\":\"\"},{\"label\":\"Self-employed/Business Owner\",\"value\":\"selfEmployed\",\"shortcut\":\"\"},{\"label\":\"Student\",\"value\":\"student\",\"shortcut\":\"\"},{\"label\":\"Unemployed\",\"value\":\"unemployed\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"employmentStatus\",\"type\":\"selectboxes\",\"input\":true,\"inputType\":\"checkbox\",\"parentPanelKey\":\"employmentInfo\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Employer's Name\",\"applyMaskOn\":\"change\",\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"employersName\",\"customConditional\":\"show = (data.employmentStatus.employed == true || data.employmentStatus.retired == true );\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"},{\"label\":\"Duration in years\",\"applyMaskOn\":\"change\",\"hidden\":true,\"mask\":false,\"tableView\":false,\"delimiter\":false,\"requireDecimal\":false,\"inputFormat\":\"plain\",\"truncateMultipleSpaces\":false,\"validate\":{\"required\":true},\"key\":\"durationInYears\",\"customConditional\":\"show = (data.employmentStatus.employed == true || data.employmentStatus.retired == true);\",\"type\":\"number\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"},{\"label\":\"Country\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"retiredCountry\",\"customConditional\":\"show = (data.employmentStatus.retired == true);\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=country'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"employmentInfo\"},{\"label\":\"Customer's Occupation\",\"applyMaskOn\":\"change\",\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"customersOccupation\",\"conditional\":{\"show\":true,\"when\":\"employmentStatus\",\"eq\":\"employed\"},\"customConditional\":\"show = (data.employmentStatus.employed == true || data.employmentStatus.retired == true );\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"},{\"label\":\"Other\",\"applyMaskOn\":\"change\",\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"otherEmployment\",\"conditional\":{\"show\":true,\"when\":\"employmentStatus\",\"eq\":\"other\"},\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Business Name\",\"applyMaskOn\":\"change\",\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"businessName\",\"customConditional\":\"show = (data.employmentStatus.selfEmployed == true);\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"},{\"label\":\"Select High Risk Industry (if applicable)\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Adult Entertainment\",\"value\":\"Adult Entertainment\"},{\"label\":\"Aerospace\",\"value\":\"Aerospace\"},{\"label\":\"Arms & Defense\",\"value\":\"Arms & Defense\"},{\"label\":\"Cash Intensive Business\",\"value\":\"Cash Intensive Business\"},{\"label\":\"Casino / Gaming Establishment\",\"value\":\"Casino / Gaming Establishment\"},{\"label\":\"Chemicals\",\"value\":\"Chemicals\"},{\"label\":\"Construction or Public Works\",\"value\":\"Construction or Public Works\"},{\"label\":\"Correspondent Bank (Domestic or Foreign)\",\"value\":\"Correspondent Bank (Domestic or Foreign)\"},{\"label\":\"Extractive\",\"value\":\"Extractive\"},{\"label\":\"FinTech\",\"value\":\"FinTech\"},{\"label\":\"Government and Government Owned\",\"value\":\"Government and Government Owned\"},{\"label\":\"Heavy Engineering / Heavy Machinery\",\"value\":\"Heavy Engineering / Heavy Machinery\"},{\"label\":\"Hedge Fund\",\"value\":\"Hedge Fund\"},{\"label\":\"Independent ATM\",\"value\":\"Independent ATM\"},{\"label\":\"Investment Company (Non-Fund SPV/SPE)\",\"value\":\"Investment Company (Non-Fund SPV/SPE)\"},{\"label\":\"Investment Company - PIC\",\"value\":\"Investment Company - PIC\"},{\"label\":\"Marijuana Related Business (MRB)\",\"value\":\"Marijuana Related Business (MRB)\"},{\"label\":\"Marijuana Related Business Indirect Participants\",\"value\":\"Marijuana Related Business Indirect Participants\"},{\"label\":\"Money Service Business\",\"value\":\"Money Service Business\"},{\"label\":\"Non Correspondent Bank(Domestic or Foreign)\",\"value\":\"Non Correspondent Bank(Domestic or Foreign)\"},{\"label\":\"Non-Bank Financial Institution - Cash\",\"value\":\"Non-Bank Financial Institution - Cash\"},{\"label\":\"Non-Bank Financial Institution - FI\",\"value\":\"Non-Bank Financial Institution - FI\"},{\"label\":\"Non-Profit Organization / Charity\",\"value\":\"Non-Profit Organization / Charity\"},{\"label\":\"Pharma / Medical Supplies & Technology\",\"value\":\"Pharma / Medical Supplies & Technology\"},{\"label\":\"Private Equity Fund\",\"value\":\"Private Equity Fund\"},{\"label\":\"Professional Service Provider acting as a Financial Intermediary\",\"value\":\"Professional Service Provider acting as a Financial Intermediary\"},{\"label\":\"Quasi-Governmental/Supra National Organization\",\"value\":\"Quasi-Governmental/Supra National Organization\"},{\"label\":\"Shipping / Transportation\",\"value\":\"Shipping / Transportation\"},{\"label\":\"Telecom\",\"value\":\"Telecom\"},{\"label\":\"Third Party Payment Processor\",\"value\":\"Third Party Payment Processor\"},{\"label\":\"Utilities\",\"value\":\"Utilities\"},{\"label\":\"Virtual Asset Service Providers\",\"value\":\"Virtual Asset Service Providers\"}]},\"key\":\"selfEmployedHighRisk\",\"customConditional\":\"show = (data.employmentStatus.selfEmployed == true);\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"key\":\"columns4\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"title\":\"Employment Address\",\"collapsible\":false,\"key\":\"employmentAddress\",\"conditional\":{\"show\":true,\"when\":\"employmentStatus\",\"eq\":\"employed\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Address Line 1\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"employerAddress1\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentAddress\"},{\"label\":\"Address Line 2\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"employerAddress2\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentAddress\"},{\"label\":\"Address Line 3\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"employerAddress3\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentAddress\"}],\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4,\"width\":4},{\"components\":[{\"label\":\"City\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"employerCity\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentAddress\"},{\"label\":\"State\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"label\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"employerState\",\"conditional\":{\"show\":true,\"when\":\"employerCountry\",\"eq\":\"United States Of America\"},\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=employerState'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"employmentAddress\"}],\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4,\"width\":4},{\"components\":[{\"label\":\"Country\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"employerCountry\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=employerCountry'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"employmentAddress\"},{\"label\":\"Postal Code\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"employerPostalCode\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"employmentAddress\"}],\"size\":\"md\",\"width\":4,\"currentWidth\":4}],\"key\":\"columns5\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Is the client a current or former Senior United States or Non-USA Official / also known as a Politically Exposed Person (PEP), related to a PEP, or closely associated with a PEP?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"indivPEP\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"},{\"label\":\"Are any of the beneficial owners/authorized signers or other individuals with authority over this entity a current or former Senior United States or Non-USA Official / also known as a Politically Exposed Person (PEP), related to a PEP, or closely associated with a PEP?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"entityPEP\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"employmentInfo\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns6\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"Website Address\",\"collapsible\":false,\"key\":\"websiteAddress1\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Does the customer have a website?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"radioWebsite\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"websiteAddress1\"},{\"label\":\"Website Address\",\"applyMaskOn\":\"change\",\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"websiteAddress\",\"conditional\":{\"show\":true,\"when\":\"radioWebsite\",\"eq\":\"yes\"},\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"websiteAddress1\"}]},{\"title\":\"Institutional Classification\",\"collapsible\":false,\"key\":\"institutionalClassification\",\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Is the Client relationship associated to the Institutional Wealth Management Line of Business (Incl GIO and EFG)?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"defaultValue\":\"no\",\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"clearOnHide\":false,\"validate\":{\"required\":true},\"key\":\"isIWM\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"institutionalClassification\"},{\"label\":\"Is the client considered an institutional client (FINRA Reg 2111, MIFID, SFC or MAS)?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"defaultValue\":\"no\",\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"clearOnHide\":false,\"validate\":{\"required\":true},\"key\":\"isInstitutional\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"institutionalClassification\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}]},{\"label\":\"KYC Details\",\"key\":\"kycDetails\",\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Ownership Type\",\"widget\":\"choicesjs\",\"tableView\":true,\"defaultValue\":\"private\",\"data\":{\"values\":[{\"label\":\"Public\",\"value\":\"public\"},{\"label\":\"Private\",\"value\":\"private\"}]},\"validate\":{\"required\":true},\"key\":\"ownershipType\",\"type\":\"select\",\"input\":true},{\"label\":\"Is the Client engaged in business with any of the following high risk industries, selection may drive SpDD\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Adult Entertainment\",\"value\":\"Adult Entertainment\"},{\"label\":\"Aerospace\",\"value\":\"Aerospace\"},{\"label\":\"Arms & Defense\",\"value\":\"Arms & Defense\"},{\"label\":\"Cash Intensive Business\",\"value\":\"Cash Intensive Business\"},{\"label\":\"Casino / Gaming Establishment\",\"value\":\"Casino / Gaming Establishment\"},{\"label\":\"Chemicals\",\"value\":\"Chemicals\"},{\"label\":\"Construction or Public Works\",\"value\":\"Construction or Public Works\"},{\"label\":\"Correspondent Bank (Domestic or Foreign)\",\"value\":\"Correspondent Bank (Domestic or Foreign)\"},{\"label\":\"Extractive\",\"value\":\"Extractive\"},{\"label\":\"FinTech\",\"value\":\"FinTech\"},{\"label\":\"Government and Government Owned\",\"value\":\"Government and Government Owned\"},{\"label\":\"Heavy Engineering / Heavy Machinery\",\"value\":\"Heavy Engineering / Heavy Machinery\"},{\"label\":\"Hedge Fund\",\"value\":\"Hedge Fund\"},{\"label\":\"Independent ATM\",\"value\":\"Independent ATM\"},{\"label\":\"Investment Company (Non-Fund SPV/SPE)\",\"value\":\"Investment Company (Non-Fund SPV/SPE)\"},{\"label\":\"Investment Company - PIC\",\"value\":\"Investment Company - PIC\"},{\"label\":\"Marijuana Related Business (MRB)\",\"value\":\"Marijuana Related Business (MRB)\"},{\"label\":\"Marijuana Related Business Indirect Participants\",\"value\":\"Marijuana Related Business Indirect Participants\"},{\"label\":\"Money Service Business\",\"value\":\"Money Service Business\"},{\"label\":\"Non Correspondent Bank(Domestic or Foreign)\",\"value\":\"Non Correspondent Bank(Domestic or Foreign)\"},{\"label\":\"Non-Bank Financial Institution - Cash\",\"value\":\"Non-Bank Financial Institution - Cash\"},{\"label\":\"Non-Bank Financial Institution - FI\",\"value\":\"Non-Bank Financial Institution - FI\"},{\"label\":\"Non-Profit Organization / Charity\",\"value\":\"Non-Profit Organization / Charity\"},{\"label\":\"Pharma / Medical Supplies & Technology\",\"value\":\"Pharma / Medical Supplies & Technology\"},{\"label\":\"Private Equity Fund\",\"value\":\"Private Equity Fund\"},{\"label\":\"Professional Service Provider acting as a Financial Intermediary\",\"value\":\"Professional Service Provider acting as a Financial Intermediary\"},{\"label\":\"Quasi-Governmental/Supra National Organization\",\"value\":\"Quasi-Governmental/Supra National Organization\"},{\"label\":\"Shipping / Transportation\",\"value\":\"Shipping / Transportation\"},{\"label\":\"Telecom\",\"value\":\"Telecom\"},{\"label\":\"Third Party Payment Processor\",\"value\":\"Third Party Payment Processor\"},{\"label\":\"Utilities\",\"value\":\"Utilities\"},{\"label\":\"Virtual Asset Service Providers\",\"value\":\"Virtual Asset Service Providers\"}]},\"key\":\"highRiskIndustry\",\"type\":\"select\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[{\"label\":\"Is this KYC for a non-customer sponsor of a Special Purpose Vehicle (SPV) Client?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"spvSponsor\",\"type\":\"radio\",\"input\":true},{\"label\":\"Is the Trust Revocable or Irrevocable\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"values\":[{\"label\":\"Revocable\",\"value\":\"revocable\",\"shortcut\":\"\"},{\"label\":\"Irrevocable\",\"value\":\"irrevocable\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"revocableIrrevocable\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"yes\"},\"type\":\"radio\",\"input\":true},{\"label\":\"Is the client a statutory trust?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"hidden\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"statutoryTrust\",\"conditional\":{\"show\":true,\"when\":\"isTrust\",\"eq\":\"yes\"},\"type\":\"radio\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns27\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"entity\"},\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Is the client a prohibited individual or entity client type or operating/providing prohibited services?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"clientProhibited\",\"type\":\"radio\",\"input\":true},{\"label\":\"Please select from the following Firm-Wide prohibition and PB/JPMA Highly Restricted Client Types and Services\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Adult Entertainment Businesses\",\"value\":\"adultEntertainmentBusinesses\"},{\"label\":\"Arms, Ammunition and Explosive Companies\",\"value\":\"armsAmmunitionAndExplosiveCompanies\"},{\"label\":\"Bank Note Trading Businesses\",\"value\":\"bankNoteTradingBusinesses\"},{\"label\":\"Banks (only permitted under certain conditions)\",\"value\":\"banksOnlyPermittedUnderCertainConditions\"},{\"label\":\"Casinos and Other Gaming Commissions\",\"value\":\"casinosAndOtherGamingCommissions\"},{\"label\":\"Clients reselling their services to a 3rd party w/in JPMC account (Refer to MS63 Appendix B1 for details)\",\"value\":\"clientsResellingTheirServicesToA3rdPartyWInJpmcAccountReferToMs63AppendixB1ForDetails\"},{\"label\":\"Internet Gambling Businesses\",\"value\":\"internetGamblingBusinesses\"},{\"label\":\"Marijuana-related business - Any\",\"value\":\"marijuanaRelatedBusinessAny\"},{\"label\":\"Marijuana-related businesses (including MRB IPs) that are prohibited under Section 7 of the GKYCS\",\"value\":\"marijuanaRelatedBusinessesIncludingMrbIPsThatAreProhibitedUnderSection7OfTheGkycs\"},{\"label\":\"MSBs (T-MSBs and FinTech MSBs) (including casas de cambio) from very high countries\",\"value\":\"msBsTMsBsAndFinTechMsBsIncludingCasasDeCambioFromVeryHighCountries\"},{\"label\":\"New Bearer Shares Companies, except those publicly traded on a level 1 exchange\",\"value\":\"newBearerSharesCompaniesExceptThosePubliclyTradedOnALevel1Exchange\"},{\"label\":\"Non-US Embassies, missions, and consulates\",\"value\":\"nonUsEmbassiesMissionsAndConsulates\"},{\"label\":\"PACS (Political Action Committees)\",\"value\":\"pacsPoliticalActionCommittees\"},{\"label\":\"Pawn Shops / Pawn Brokers\",\"value\":\"pawnShopsPawnBrokers\"},{\"label\":\"Payday Lenders\",\"value\":\"paydayLenders\"},{\"label\":\"Pre-Paid Access / Stored Value Cards\",\"value\":\"prePaidAccessStoredValueCards\"},{\"label\":\"Sovereign Nations\",\"value\":\"sovereignNations\"},{\"label\":\"Telemarketing Businesses\",\"value\":\"telemarketingBusinesses\"},{\"label\":\"Third Party Payment Processors (TPPPs)\",\"value\":\"thirdPartyPaymentProcessorsTppPs\"},{\"label\":\"Virtual Asset Service Providers or other entities that are prohibited under Section 7 of the GKYCS\",\"value\":\"virtualAssetServiceProvidersOrOtherEntitiesThatAreProhibitedUnderSection7OfTheGkycs\"}]},\"validate\":{\"required\":true},\"key\":\"prohibitedClientType\",\"conditional\":{\"show\":true,\"when\":\"clientProhibited\",\"eq\":\"yes\"},\"type\":\"select\",\"input\":true},{\"label\":\"During the course of business, has it been determined that the customer is an owner, provider, and/or operator of independent ATM(s)?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"ownerATM\",\"type\":\"radio\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns26\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Radio\",\"optionsLabelPosition\":\"bottom\",\"inline\":true,\"hideLabel\":true,\"tableView\":false,\"defaultValue\":\"estimated\",\"values\":[{\"label\":\"Actual\",\"value\":\"actual\",\"shortcut\":\"\"},{\"label\":\"Estimated\",\"value\":\"estimated\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"actualEstimated\",\"type\":\"radio\",\"input\":true},{\"label\":\"Fiscal Year End Date\",\"format\":\"yyyy-MM-dd \",\"tableView\":false,\"datePicker\":{\"disableWeekends\":false,\"disableWeekdays\":false},\"enableTime\":false,\"validate\":{\"required\":true},\"enableMinDateInput\":false,\"enableMaxDateInput\":false,\"key\":\"fiscalYearEnd\",\"type\":\"datetime\",\"input\":true,\"widget\":{\"type\":\"calendar\",\"displayInTimezone\":\"viewer\",\"locale\":\"en\",\"useLocaleSettings\":false,\"allowInput\":true,\"mode\":\"single\",\"enableTime\":false,\"noCalendar\":false,\"format\":\"yyyy-MM-dd \",\"hourIncrement\":1,\"minuteIncrement\":1,\"time_24hr\":false,\"minDate\":null,\"disableWeekends\":false,\"disableWeekdays\":false,\"maxDate\":null}},{\"label\":\"Total Assets in USD\",\"prefix\":\"$\",\"applyMaskOn\":\"change\",\"hidden\":true,\"mask\":false,\"tableView\":false,\"delimiter\":false,\"requireDecimal\":false,\"inputFormat\":\"plain\",\"truncateMultipleSpaces\":false,\"validate\":{\"required\":true},\"key\":\"totalAssets\",\"conditional\":{\"show\":true,\"when\":\"naicCode\",\"eq\":\"pic\"},\"type\":\"number\",\"input\":true},{\"label\":\"Total Annual Revenue/Income\",\"prefix\":\"$\",\"applyMaskOn\":\"change\",\"hidden\":true,\"mask\":false,\"tableView\":false,\"delimiter\":false,\"requireDecimal\":false,\"inputFormat\":\"plain\",\"truncateMultipleSpaces\":false,\"validate\":{\"required\":true},\"key\":\"totalAnnualRevenue\",\"conditional\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"operatingCompany\"},\"type\":\"number\",\"input\":true},{\"label\":\"Country(ies) of Significant Business Operations\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryOfOperations\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryOfOperations'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true},{\"label\":\"Country(ies) of significant vendors and suppliers\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryOfVendors\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryOfVendors'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true},{\"label\":\"Country(ies) of Client's Significant Clients\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryOfClients\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryOfClients'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[{\"label\":\"Provide a description of the origin/source of capital for the entity\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"capitalOrigin\",\"conditional\":{\"show\":true,\"when\":\"naicCode\",\"eq\":\"pic\"},\"type\":\"textarea\",\"input\":true},{\"label\":\"Describe the client's major clients\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"hidden\":true,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"majorClients\",\"conditional\":{\"show\":true,\"when\":\"customerEntityType\",\"eq\":\"operatingCompany\"},\"type\":\"textarea\",\"input\":true},{\"label\":\"Provide a detailed description of the business\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"provideADetailedDescriptionOfTheBusiness\",\"type\":\"textarea\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns20\",\"conditional\":{\"show\":true,\"when\":\"naicCode\",\"eq\":\"pic\"},\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"title\":\"Source of Wealth\",\"collapsible\":false,\"key\":\"sourceOfWealth1\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Total Annual Income\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"totalAnnualIncome\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Source(s) of Income\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Salary\",\"value\":\"Salary(Individual or Spousal)\"},{\"label\":\"Spousal/Family Support\",\"value\":\"Spousal/Family Support\"},{\"label\":\"Self-Employed/Business Owner\",\"value\":\"Self-Employed Income/Business Owner\"},{\"label\":\"Investments\",\"value\":\"Investments\"},{\"label\":\"Inheritance/Family Wealth\",\"value\":\"Inheritance/Family Wealth\"},{\"label\":\"Interest and Dividends\",\"value\":\"Interest and Dividends\"},{\"label\":\"Retirement/Pension\",\"value\":\"Retirement/Pension\"},{\"label\":\"Lottery\",\"value\":\"Lottery\"},{\"label\":\"Annuity\",\"value\":\"Annuity\"},{\"label\":\"Trust Income\",\"value\":\"Trust Income\"},{\"label\":\"Real Estate/Rental Income\",\"value\":\"Real Estate/Rental Income\"},{\"label\":\"Government Benefits\",\"value\":\"Government Benefits\"},{\"label\":\"Legal Settlement\",\"value\":\"Legal Settlement\"},{\"label\":\"Compensation\",\"value\":\"Compensation\"},{\"label\":\"Other\",\"value\":\"Other\"}]},\"validate\":{\"required\":true},\"key\":\"sourceOfIncome\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Total Investible Assets\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"totalInvestibleAssets\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[{\"label\":\"Is the Client's Significant Source of Wealth from a High Risk Industry?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"highRiskSOW\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Select High Risk Industry\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Adult Entertainment\",\"value\":\"Adult Entertainment\"},{\"label\":\"Aerospace\",\"value\":\"Aerospace\"},{\"label\":\"Arms & Defense\",\"value\":\"Arms & Defense\"},{\"label\":\"Cash Intensive Business\",\"value\":\"Cash Intensive Business\"},{\"label\":\"Casino / Gaming Establishment\",\"value\":\"Casino / Gaming Establishment\"},{\"label\":\"Chemicals\",\"value\":\"Chemicals\"},{\"label\":\"Construction or Public Works\",\"value\":\"Construction or Public Works\"},{\"label\":\"Correspondent Bank (Domestic or Foreign)\",\"value\":\"Correspondent Bank (Domestic or Foreign)\"},{\"label\":\"Extractive\",\"value\":\"Extractive\"},{\"label\":\"FinTech\",\"value\":\"FinTech\"},{\"label\":\"Government and Government Owned\",\"value\":\"Government and Government Owned\"},{\"label\":\"Heavy Engineering / Heavy Machinery\",\"value\":\"Heavy Engineering / Heavy Machinery\"},{\"label\":\"Hedge Fund\",\"value\":\"Hedge Fund\"},{\"label\":\"Independent ATM\",\"value\":\"Independent ATM\"},{\"label\":\"Investment Company (Non-Fund SPV/SPE)\",\"value\":\"Investment Company (Non-Fund SPV/SPE)\"},{\"label\":\"Investment Company - PIC\",\"value\":\"Investment Company - PIC\"},{\"label\":\"Marijuana Related Business (MRB)\",\"value\":\"Marijuana Related Business (MRB)\"},{\"label\":\"Marijuana Related Business Indirect Participants\",\"value\":\"Marijuana Related Business Indirect Participants\"},{\"label\":\"Money Service Business\",\"value\":\"Money Service Business\"},{\"label\":\"Non Correspondent Bank(Domestic or Foreign)\",\"value\":\"Non Correspondent Bank(Domestic or Foreign)\"},{\"label\":\"Non-Bank Financial Institution - Cash\",\"value\":\"Non-Bank Financial Institution - Cash\"},{\"label\":\"Non-Bank Financial Institution - FI\",\"value\":\"Non-Bank Financial Institution - FI\"},{\"label\":\"Non-Profit Organization / Charity\",\"value\":\"Non-Profit Organization / Charity\"},{\"label\":\"Pharma / Medical Supplies & Technology\",\"value\":\"Pharma / Medical Supplies & Technology\"},{\"label\":\"Private Equity Fund\",\"value\":\"Private Equity Fund\"},{\"label\":\"Professional Service Provider acting as a Financial Intermediary\",\"value\":\"Professional Service Provider acting as a Financial Intermediary\"},{\"label\":\"Quasi-Governmental/Supra National Organization\",\"value\":\"Quasi-Governmental/Supra National Organization\"},{\"label\":\"Shipping / Transportation\",\"value\":\"Shipping / Transportation\"},{\"label\":\"Telecom\",\"value\":\"Telecom\"},{\"label\":\"Third Party Payment Processor\",\"value\":\"Third Party Payment Processor\"},{\"label\":\"Utilities\",\"value\":\"Utilities\"},{\"label\":\"Virtual Asset Service Providers\",\"value\":\"Virtual Asset Service Providers\"}]},\"validate\":{\"required\":true},\"key\":\"sowHighRiskIndustry\",\"conditional\":{\"show\":true,\"when\":\"highRiskSOW\",\"eq\":\"yes\"},\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns19\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"What are the sources of wealth?\",\"optionsLabelPosition\":\"bottom\",\"tableView\":false,\"values\":[{\"label\":\"Employment\",\"value\":\"employment\",\"shortcut\":\"\"},{\"label\":\"Business Ownership\",\"value\":\"businessOwnership\",\"shortcut\":\"\"},{\"label\":\"Inheritance/Gift from deceased person\",\"value\":\"inheritance\",\"shortcut\":\"\"},{\"label\":\"Sale of Assets or Business\",\"value\":\"saleOfAssets\",\"shortcut\":\"\"},{\"label\":\"Investments/Appreciation\",\"value\":\"investments\",\"shortcut\":\"\"},{\"label\":\"Other source\",\"value\":\"otherSource\",\"shortcut\":\"\"},{\"label\":\"Another Living Person\",\"value\":\"otherPerson\",\"shortcut\":\"\"}],\"allowCalculateOverride\":true,\"validate\":{\"required\":true},\"key\":\"sourceOfWealth\",\"type\":\"selectboxes\",\"input\":true,\"inputType\":\"checkbox\",\"defaultValue\":{\"employment\":false,\"businessOwnership\":false,\"inheritance\":false,\"saleOfAssets\":false,\"investments\":false,\"otherSource\":false,\"otherPerson\":false},\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns21\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"employment\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Employment</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"nameOfEmployer\":\"\",\"descriptionOfTheBusiness\":\"\",\"yearsOfService\":\"\",\"positionsHeldAndTenure\":\"\",\"approximateAnnualSalary\":\"\"}],\"key\":\"employment\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"employment\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Name of Employer\",\"applyMaskOn\":\"change\",\"tableView\":true,\"clearOnHide\":false,\"calculateValue\":\"value = (data.employersName)\",\"allowCalculateOverride\":true,\"validate\":{\"required\":true},\"key\":\"nameOfEmployer\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Description of the business \",\"description\":\"(i.e. history of the business including notable products/services, areas of operation, and types of clients served)\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"descriptionOfTheBusiness\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3,\"width\":3},{\"components\":[{\"label\":\"Years of service in the industry\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"yearsOfService\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Approximate annual salary/bonus history\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateAnnualSalary\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Positions(s) held and tenure\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"positionsHeldAndTenure\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"attributes\":{\"style\":\"margin-bottom:20px\"},\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html1\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Business Ownership</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"companyName\":\"\",\"numberOfLocations\":\"\",\"natureOfBusiness\":{},\"numberOfEmployees\":\"\",\"yearEstablished\":\"00/00/0000\",\"currentValueOfTheBusiness\":\"\",\"profitMargin\":\"\",\"estimatedAnnualNetIncome\":\"\",\"clientsNotableProducts\":\"\",\"geographyOfMarkets\":[],\"approximateInitialInvestment\":\"\"}],\"key\":\"businessOwnership\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"businessOwnership\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Company name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"clearOnHide\":false,\"calculateValue\":\"value = (data.businessName)\",\"allowCalculateOverride\":true,\"validate\":{\"required\":true},\"key\":\"companyName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Number of stores, offices, and locations\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"numberOfLocations\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Nature of business\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"validate\":{\"required\":true},\"key\":\"natureOfBusiness\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 1\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=natureOfBusiness'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Number of Employees\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"numberOfEmployees\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Client's notable products, services, and clients\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"clientsNotableProducts\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Year Established\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearEstablished\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Current value of the business\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"currentValueOfTheBusiness\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Profit Margin (estimated), % holdings of the business\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"profitMargin\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Estimated Annual Net Income/Sales from business/Annual turnover\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAnnualNetIncome\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Geography of the markets in which the business operates and where the clients are located\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"validate\":{\"required\":true,\"multiple\":true},\"key\":\"geographyOfMarkets\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=geographyOfMarkets'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Approximate initial investment and source\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateInitialInvestment\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html5\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"inheritance\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Inheritance/Gift</strong>\",\"reorder\":false,\"addAnotherPosition\":\"bottom\",\"addAnother\":\"Add Entry\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"firstName\":\"\",\"middleName\":\"\",\"lastName\":\"\",\"otherLegalNames\":\"\",\"description\":\"\",\"generation\":\"\",\"suffix\":\"\",\"gender\":\"\",\"countryOfLastKnownResidence\":\"\",\"natureOfTheAssetReceived\":\"\",\"relationshipToGiftingParty\":\"\",\"whenWasGiftOrInheritanceReceived\":\"\",\"estimatedAmountReceived\":\"\",\"estimatedPresentValue\":\"\",\"additionalInvestmentRentalIncome\":\"\"}],\"key\":\"inheritanceGift\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"inheritance\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"First Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"firstName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Middle Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"middleName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Last Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"lastName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Other Legal Names (Previous Name / Alias)\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"otherLegalNames\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Description - Other Legal Names (Previous Name / Alias)\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"description\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Generation\",\"widget\":\"choicesjs\",\"tableView\":true,\"key\":\"generation\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Suffix\",\"widget\":\"choicesjs\",\"tableView\":true,\"key\":\"suffix\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Gender\",\"widget\":\"choicesjs\",\"tableView\":true,\"key\":\"gender\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Country of last known residence\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryOfLastKnownResidence\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryOfLastKnownResidence'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Nature of the asset received (cash, real estate, stock, etc.)\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"natureOfTheAssetReceived\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Relationship between the client and the gifting party\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"relationshipToGiftingParty\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"When was the gift or inheritance received\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"whenWasGiftOrInheritanceReceived\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Estimated amount received\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAmountReceived\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Estimated present value\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedPresentValue\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Additional investment/rental income\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"additionalInvestmentRentalIncome\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html2\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"saleOfAssets\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Sale of Assets/Business</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"companyName\":\"\",\"countriesOfOperation\":[],\"yearSold\":\"00/00/0000\",\"approximateSalePrice\":\"\",\"estimatedAmountOfSale\":\"\",\"estimatedInitialPurchaseSetupAmount\":\"\",\"describeRealEstate\":\"\"}],\"key\":\"saleOfAssetsBusiness\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"saleOfAssets\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Company Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"companyName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Countries of operation\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false,\"multiple\":true},\"key\":\"countriesOfOperation\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countriesOfOperation'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Year the business was sold\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearSold\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Approximate Sale Price\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateSalePrice\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Estimated amount of sale/Current market value\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAmountOfSale\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Estimated initial purchase/setup amount\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedInitialPurchaseSetupAmount\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"If related to real estate properties, describe the location, size, and year purchased\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeRealEstate\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html3\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"investmentsAppreciation\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong> Investments/Appreciation</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"descriptionOfTheInvestments\":\"\",\"describeAppreciation\":\"\",\"assetType\":{\"physicalAsset\":false,\"investibleAsset\":false},\"yearTheBusinessWasSold\":\"00/00/0000\",\"additionalInvestmentRentalIncome\":\"\",\"estimatedAmountOfSale\":\"\",\"estimatedInitialPurchaseSetupAmount\":\"\",\"approximateSalePrice\":\"\",\"describeRealEstate\":\"\"}],\"key\":\"investmentsAppreciation\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"investments\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Description of the investments and assets\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"descriptionOfTheInvestments\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Describe Appreciation\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeAppreciation\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Asset Type\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Physical Asset\",\"value\":\"physicalAsset\",\"shortcut\":\"\"},{\"label\":\"Investible Asset\",\"value\":\"investibleAsset\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"assetType\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Year the business was sold\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"type\":\"select\",\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearTheBusinessWasSold\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Additional investment/rental income\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"additionalInvestmentRentalIncome\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Estimated amount of sale/Current market value\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAmountOfSale\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Estimated initial purchase/setup amount\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedInitialPurchaseSetupAmount\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"},{\"label\":\"Approximate Sale Price\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateSalePrice\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"If related to real estate properties, describe the location, size, and year purchased\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeRealEstate\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html4\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"otherSource\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Other Income</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{}],\"key\":\"otherIncome\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"otherSource\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Describe the source\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeTheSource\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3,\"width\":3},{\"components\":[{\"label\":\"Country\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false,\"multiple\":true},\"key\":\"otherSourceCountry\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=otherSourceCountry'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"What is the amount received?\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"whatIsTheAmountReceived\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Year received\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"type\":\"select\",\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearReceived\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"sourceOfWealth1\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"Another Living Person\",\"customClass\":\"noBorderPanel\",\"collapsible\":false,\"key\":\"anotherLivingPerson\",\"conditional\":{\"show\":true,\"when\":\"sourceOfWealth\",\"eq\":\"otherPerson\"},\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"ECI of Individual\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"eciOfIndividual1\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Name of Individual\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"nameOfIndividual\",\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4},{\"components\":[{\"label\":\"Is the Client's Significant Source of Wealth from a High Risk Industry?\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Yes\",\"value\":\"yes\",\"shortcut\":\"\"},{\"label\":\"No\",\"value\":\"no\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"highRiskSOWOther\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Select High Risk Industry\",\"widget\":\"choicesjs\",\"hidden\":true,\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Adult Entertainment\",\"value\":\"Adult Entertainment\"},{\"label\":\"Aerospace\",\"value\":\"Aerospace\"},{\"label\":\"Arms & Defense\",\"value\":\"Arms & Defense\"},{\"label\":\"Cash Intensive Business\",\"value\":\"Cash Intensive Business\"},{\"label\":\"Casino / Gaming Establishment\",\"value\":\"Casino / Gaming Establishment\"},{\"label\":\"Chemicals\",\"value\":\"Chemicals\"},{\"label\":\"Construction or Public Works\",\"value\":\"Construction or Public Works\"},{\"label\":\"Correspondent Bank(Domestic or Foreign)\",\"value\":\"Correspondent Bank(Domestic or Foreign)\"},{\"label\":\"Extractive\",\"value\":\"Extractive\"},{\"label\":\"FinTech\",\"value\":\"FinTech\"},{\"label\":\"Government and Government Owned\",\"value\":\"Government and Government Owned\"},{\"label\":\"Heavy Engineering / Heavy Machinery\",\"value\":\"Heavy Engineering / Heavy Machinery\"},{\"label\":\"Hedge Fund\",\"value\":\"Hedge Fund\"},{\"label\":\"Independent ATM\",\"value\":\"Independent ATM\"},{\"label\":\"Investment Company (Non-Fund SPV/SPE)\",\"value\":\"Investment Company (Non-Fund SPV/SPE)\"},{\"label\":\"Investment Company - PIC\",\"value\":\"Investment Company - PIC\"},{\"label\":\"Marijuana Related Business (MRB)\",\"value\":\"Marijuana Related Business (MRB)\"},{\"label\":\"Marijuana Related Business Indirect Participants\",\"value\":\"Marijuana Related Business Indirect Participants\"},{\"label\":\"Money Service Business\",\"value\":\"Money Service Business\"},{\"label\":\"Non Correspondent Bank(Domestic or Foreign)\",\"value\":\"Non Correspondent Bank(Domestic or Foreign)\"},{\"label\":\"Non-Bank Financial Institution - Cash\",\"value\":\"Non-Bank Financial Institution - Cash\"},{\"label\":\"Non-Bank Financial Institution - FI\",\"value\":\"Non-Bank Financial Institution - FI\"},{\"label\":\"Non-Profit Organization / Charity\",\"value\":\"Non-Profit Organization / Charity\"},{\"label\":\"Pharma / Medical Supplies & Technology\",\"value\":\"Pharma / Medical Supplies & Technology\"},{\"label\":\"Private Equity Fund\",\"value\":\"Private Equity Fund\"},{\"label\":\"Professional Service Provider acting as a Financial Intermediary\",\"value\":\"Professional Service Provider acting as a Financial Intermediary\"},{\"label\":\"Quasi-Governmental/Supra National Organization\",\"value\":\"Quasi-Governmental/Supra National Organization\"},{\"label\":\"Shipping / Transportation\",\"value\":\"Shipping / Transportation\"},{\"label\":\"Telecom\",\"value\":\"Telecom\"},{\"label\":\"Third Party Payment Processor\",\"value\":\"Third Party Payment Processor\"},{\"label\":\"Utilities\",\"value\":\"Utilities\"},{\"label\":\"Virtual Asset Service Providers\",\"value\":\"Virtual Asset Service Providers\"}]},\"validate\":{\"required\":true},\"key\":\"sowOtherHighRiskIndustry\",\"conditional\":{\"show\":true,\"when\":\"highRiskSOWOther\",\"eq\":\"yes\"},\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4},{\"components\":[{\"label\":\"What are the sources of wealth?\",\"optionsLabelPosition\":\"bottom\",\"tableView\":false,\"defaultValue\":{\"employment\":false,\"businessOwnership\":false,\"inheritanceGiftFromDeceasedPerson\":false,\"saleOfAssetsOrBusiness\":false,\"investmentsAppreciation\":false,\"otherSource\":false,\"anotherLivingPerson\":false,\"inheritance\":false,\"saleOfAssets\":false,\"investments\":false,\"otherPerson\":false},\"values\":[{\"label\":\"Employment\",\"value\":\"employment\",\"shortcut\":\"\"},{\"label\":\"Business Ownership\",\"value\":\"businessOwnership\",\"shortcut\":\"\"},{\"label\":\"Inheritance/Gift from deceased person\",\"value\":\"inheritance\",\"shortcut\":\"\"},{\"label\":\"Sale of Assets or Business\",\"value\":\"saleOfAssets\",\"shortcut\":\"\"},{\"label\":\"Investments/Appreciation\",\"value\":\"investments\",\"shortcut\":\"\"},{\"label\":\"Other source\",\"value\":\"otherSource\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"otherSourceOfWealth\",\"type\":\"selectboxes\",\"input\":true,\"inputType\":\"checkbox\",\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":4,\"currentWidth\":4}],\"key\":\"columns22\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html6\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"employment\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Employment</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"nameOfEmployer\":\"\",\"descriptionOfTheBusiness\":\"\",\"yearsOfService\":\"\",\"positionsHeldAndTenure\":\"\",\"approximateAnnualSalary\":\"\"}],\"key\":\"employmentOtherPerson\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"employment\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Name of Employer\",\"applyMaskOn\":\"change\",\"tableView\":true,\"calculateValue\":\"value = (data.employersName)\",\"allowCalculateOverride\":true,\"validate\":{\"required\":true},\"key\":\"nameOfEmployer\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Description of the business \",\"description\":\"(i.e. history of the business including notable products/services, areas of operation, and types of clients served)\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"descriptionOfTheBusiness\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3,\"width\":3},{\"components\":[{\"label\":\"Years of service in the industry\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"yearsOfService\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Approximate annual salary/bonus history\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateAnnualSalary\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Positions(s) held and tenure\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"positionsHeldAndTenure\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html7\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"businessOwnershipOtherPerson\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Business Ownership</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"companyName\":\"\",\"numberOfLocations\":\"\",\"natureOfBusiness\":{},\"numberOfEmployees\":\"\",\"yearEstablished\":\"00/00/0000\",\"currentValueOfTheBusiness\":\"\",\"profitMargin\":\"\",\"estimatedAnnualNetIncome\":\"\",\"yearEstablished1\":\"\",\"clientsNotableProducts\":\"\",\"geographyOfMarkets\":[],\"approximateInitialInvestment\":\"\"}],\"key\":\"businessOwnershipOtherPerson\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"businessOwnership\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Company name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"calculateValue\":\"value = (data.businessName)\",\"allowCalculateOverride\":true,\"validate\":{\"required\":true},\"key\":\"companyName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Number of stores, offices, and locations\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"numberOfLocations\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Nature of business\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"validate\":{\"required\":true},\"key\":\"natureOfBusiness\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 1\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=natureOfBusiness'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Year Established\",\"format\":\"yyyy\",\"tableView\":false,\"datePicker\":{\"disableWeekends\":false,\"disableWeekdays\":false},\"enableTime\":false,\"validate\":{\"required\":true},\"enableMinDateInput\":false,\"enableMaxDateInput\":false,\"key\":\"yearEstablished1\",\"type\":\"datetime\",\"input\":true,\"widget\":{\"type\":\"calendar\",\"displayInTimezone\":\"viewer\",\"locale\":\"en\",\"useLocaleSettings\":false,\"allowInput\":true,\"mode\":\"single\",\"enableTime\":false,\"noCalendar\":false,\"format\":\"yyyy\",\"hourIncrement\":1,\"minuteIncrement\":1,\"time_24hr\":false,\"minDate\":null,\"disableWeekends\":false,\"disableWeekdays\":false,\"maxDate\":null},\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Number of Employees\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"numberOfEmployees\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Client's notable products, services, and clients\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"clientsNotableProducts\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Current value of the business\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"currentValueOfTheBusiness\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Profit Margin (estimated), % holdings of the business\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"profitMargin\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Estimated Annual Net Income/Sales from business/Annual turnover\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAnnualNetIncome\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Geography of the markets in which the business operates and where the clients are located\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"validate\":{\"required\":true,\"multiple\":true},\"key\":\"geographyOfMarkets\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=geographyOfMarkets'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Approximate initial investment and source\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateInitialInvestment\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html8\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"inheritanceGiftOtherPerson\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Inheritance/Gift</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"firstName\":\"\",\"middleName\":\"\",\"lastName\":\"\",\"otherLegalNames\":\"\",\"description\":\"\",\"generation\":\"\",\"suffix\":\"\",\"gender\":\"\",\"countryOfLastKnownResidence\":\"\",\"natureOfTheAssetReceived\":\"\",\"relationshipToGiftingParty\":\"\",\"whenWasGiftOrInheritanceReceived\":\"\",\"estimatedAmountReceived\":\"\",\"estimatedPresentValue\":\"\",\"additionalInvestmentRentalIncome\":\"\"}],\"key\":\"inheritanceGiftOtherPerson\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"inheritance\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"First Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"firstName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Middle Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"middleName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Last Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"lastName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Other Legal Names (Previous Name / Alias)\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"otherLegalNames\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Description - Other Legal Names (Previous Name / Alias)\",\"applyMaskOn\":\"change\",\"tableView\":true,\"key\":\"description\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Generation\",\"widget\":\"choicesjs\",\"tableView\":true,\"key\":\"generation\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Suffix\",\"widget\":\"choicesjs\",\"tableView\":true,\"key\":\"suffix\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Gender\",\"widget\":\"choicesjs\",\"tableView\":true,\"key\":\"gender\",\"type\":\"select\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Country of last known residence\",\"widget\":\"choicesjs\",\"tableView\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false},\"key\":\"countryOfLastKnownResidence\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countryOfLastKnownResidence'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Nature of the asset received (cash, real estate, stock, etc.)\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"natureOfTheAssetReceived\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Relationship between the client and the gifting party\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"relationshipToGiftingParty\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"When was the gift or inheritance received\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"whenWasGiftOrInheritanceReceived\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Estimated amount received\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAmountReceived\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Estimated present value\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedPresentValue\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Additional investment/rental income\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"additionalInvestmentRentalIncome\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html9\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"saleOfAssetsBusinessOtherPerson\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Sale of Assets/Business</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"companyName\":\"\",\"countriesOfOperation\":[],\"yearSold\":\"00/00/0000\",\"approximateSalePrice\":\"\",\"estimatedAmountOfSale\":\"\",\"estimatedInitialPurchaseSetupAmount\":\"\",\"describeRealEstate\":\"\"}],\"key\":\"saleOfAssetsBusinessOtherPerson\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"saleOfAssets\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Company Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"companyName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Countries of operation\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false,\"multiple\":true},\"key\":\"countriesOfOperationBusiness\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=countriesOfOperationBusiness'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Year the business was sold\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"type\":\"select\",\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearSold\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Approximate Sale Price\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateSalePrice\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Estimated amount of sale/Current market value\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAmountOfSale\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Estimated initial purchase/setup amount\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedInitialPurchaseSetupAmount\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"If related to real estate properties, describe the location, size, and year purchased\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeRealEstate\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html10\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"investmentsAppreciationOtherPerson\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong> Investments/Appreciation</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"descriptionOfTheInvestments\":\"\",\"describeAppreciation\":\"\",\"assetType\":{\"physicalAsset\":false,\"investibleAsset\":false},\"yearTheBusinessWasSold\":\"00/00/0000\",\"additionalInvestmentRentalIncome\":\"\",\"estimatedAmountOfSale\":\"\",\"estimatedInitialPurchaseSetupAmount\":\"\",\"approximateSalePrice\":\"\",\"describeRealEstate\":\"\"}],\"key\":\"investmentsAppreciationOtherPerson\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"investments\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Description of the investments and assets\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"descriptionOfTheInvestments\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Describe Appreciation\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeAppreciation\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Asset Type\",\"optionsLabelPosition\":\"right\",\"inline\":true,\"tableView\":false,\"values\":[{\"label\":\"Physical Asset\",\"value\":\"physicalAsset\",\"shortcut\":\"\"},{\"label\":\"Investible Asset\",\"value\":\"investibleAsset\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"assetType\",\"type\":\"radio\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Year the business was sold\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"type\":\"select\",\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearTheBusinessWasSold\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Additional investment/rental income\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"additionalInvestmentRentalIncome\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Estimated amount of sale/Current market value\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedAmountOfSale\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Estimated initial purchase/setup amount\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"estimatedInitialPurchaseSetupAmount\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"},{\"label\":\"Approximate Sale Price\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"approximateSalePrice\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"If related to real estate properties, describe the location, size, and year purchased\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeRealEstate\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html11\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"otherIncomeOtherPerson\"},\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"<strong>Other Income</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{}],\"key\":\"otherIncomeOtherPerson\",\"conditional\":{\"show\":true,\"when\":\"otherSourceOfWealth\",\"eq\":\"otherSource\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Describe the source\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"describeTheSource\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3,\"width\":3},{\"components\":[{\"label\":\"Country\",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"dataSrc\":\"url\",\"data\":{\"headers\":[{\"key\":\"\",\"value\":\"\"}]},\"dataType\":\"string\",\"idPath\":\"\",\"valueProperty\":\"value\",\"validate\":{\"required\":true,\"select\":false,\"multiple\":true},\"key\":\"otherSourceCountry\",\"logic\":[{\"name\":\"ECIPresent\",\"trigger\":{\"type\":\"javascript\",\"javascript\":\"result = data['attributes'] && typeof data['attributes']['eci'] === 'string' && data['attributes']['eci'].trim().length > 0\"},\"actions\":[{\"name\":\"ECIPresentAction\",\"type\":\"mergeComponentSchema\",\"schemaDefinition\":\"schema = {'data':{url:'https://form-service-pba.test.gaiacloud.jpmchase.net/api/form/executeService?formId={{data.attributes.formId}}&activityId={{data.attributes.activityId}}&eci={{data.attributes.eci}}&serviceKey=otherSourceCountry'}}\"}]}],\"type\":\"select\",\"selectValues\":\"data.FETCH_MERIDIAN_GRAPHQL\",\"disableLimit\":false,\"searchField\":\"search\",\"noRefreshOnScroll\":false,\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"What is the amount received?\",\"applyMaskOn\":\"change\",\"autoExpand\":false,\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"whatIsTheAmountReceived\",\"type\":\"textarea\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"Year received\",\"hideInputLabels\":false,\"inputsLabelPosition\":\"top\",\"useLocaleSettings\":false,\"tableView\":false,\"fields\":{\"day\":{\"hide\":true},\"month\":{\"hide\":true},\"year\":{\"type\":\"select\",\"hide\":false,\"required\":true}},\"defaultValue\":\"00/00/0000\",\"key\":\"yearReceived\",\"type\":\"day\",\"input\":true,\"parentPanelKey\":\"anotherLivingPerson\"}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}]}]}],\"input\":true,\"tableView\":false},{\"label\":\"Relationships\",\"key\":\"relationships\",\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Accounts with Other Banks\",\"optionsLabelPosition\":\"right\",\"inline\":false,\"tableView\":false,\"values\":[{\"label\":\"Yes - and willing to provide the institutions\",\"value\":\"yesWilling\",\"shortcut\":\"\"},{\"label\":\"Acknowledge he/she has account(s) with other banks - but unwilling to provide the institutions\",\"value\":\"acknowledgeUnwilling\",\"shortcut\":\"\"},{\"label\":\"No - the Client does not have Accounts with other Banks\",\"value\":\"noAccounts\",\"shortcut\":\"\"},{\"label\":\"Client is unwilling to provide the information\",\"value\":\"unwillingToProvide\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"accountsWithOtherBanks\",\"type\":\"radio\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns24\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"refreshOnChange\":false,\"key\":\"html5\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"<strong>Other Institutions</strong>\",\"reorder\":false,\"addAnother\":\"Add Entry\",\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"customClass\":\"noBorderGrid\",\"tableView\":false,\"defaultValue\":[{\"institutionName\":\"\"}],\"key\":\"otherInstitutions\",\"conditional\":{\"show\":true,\"when\":\"accountsWithOtherBanks\",\"eq\":\"yesWilling\"},\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Institution Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"institutionName\",\"includeWorkflowRouting\":false,\"type\":\"textfield\",\"input\":true}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"hideLabel\":true,\"key\":\"columns\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns25\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"How was the relationship with the client established?\",\"optionsLabelPosition\":\"right\",\"inline\":false,\"tableView\":false,\"values\":[{\"label\":\"Branch\",\"value\":\"branch\",\"shortcut\":\"\"},{\"label\":\"Online/Digital\",\"value\":\"onlineDigital\",\"shortcut\":\"\"},{\"label\":\"Telephone Banking\",\"value\":\"telephoneBanking\",\"shortcut\":\"\"},{\"label\":\"In-Person\",\"value\":\"inPerson\",\"shortcut\":\"\"},{\"label\":\"JPMC Office\",\"value\":\"jpmcOffice\",\"shortcut\":\"\"},{\"label\":\"Face-to-Face\",\"value\":\"faceToFace\",\"shortcut\":\"\"},{\"label\":\"Email / Fax / Mail\",\"value\":\"emailFaxMail\",\"shortcut\":\"\"},{\"label\":\"Not Applicable\",\"value\":\"notApplicable\",\"shortcut\":\"\"},{\"label\":\"Other\",\"value\":\"other\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"relationshipEstablished\",\"attributes\":{\"display\":\"inline-block\"},\"type\":\"radio\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[{\"label\":\"Meeting Method\",\"optionsLabelPosition\":\"right\",\"inline\":false,\"tableView\":false,\"values\":[{\"label\":\"In Person\",\"value\":\"inPerson\",\"shortcut\":\"\"},{\"label\":\"Firm Approved Video Conferencing\",\"value\":\"firmApprovedVideoConferencing\",\"shortcut\":\"\"}],\"validate\":{\"required\":true},\"key\":\"meetingMethod\",\"type\":\"radio\",\"input\":true}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns28\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Location\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"location\",\"type\":\"textfield\",\"input\":true}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"Date\",\"format\":\"yyyy-MM-dd\",\"tableView\":false,\"datePicker\":{\"disableWeekends\":false,\"disableWeekdays\":false},\"enableTime\":false,\"validate\":{\"required\":true},\"enableMinDateInput\":false,\"enableMaxDateInput\":false,\"key\":\"date\",\"type\":\"datetime\",\"input\":true,\"widget\":{\"type\":\"calendar\",\"displayInTimezone\":\"viewer\",\"locale\":\"en\",\"useLocaleSettings\":false,\"allowInput\":true,\"mode\":\"single\",\"enableTime\":false,\"noCalendar\":false,\"format\":\"yyyy-MM-dd\",\"hourIncrement\":1,\"minuteIncrement\":1,\"time_24hr\":false,\"minDate\":null,\"disableWeekends\":false,\"disableWeekdays\":false,\"maxDate\":null}}],\"width\":3,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":3},{\"components\":[{\"label\":\"JPMC Participant SID\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"jpmcParticipantSid\",\"type\":\"textfield\",\"input\":true}],\"size\":\"md\",\"width\":3,\"currentWidth\":3},{\"components\":[{\"label\":\"JPMC Participant Name\",\"applyMaskOn\":\"change\",\"tableView\":true,\"validate\":{\"required\":true},\"key\":\"jpmcParticipantName\",\"type\":\"textfield\",\"input\":true}],\"size\":\"md\",\"width\":3,\"currentWidth\":3}],\"key\":\"columns29\",\"type\":\"columns\",\"input\":false,\"tableView\":false}],\"width\":12,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":12},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns23\",\"conditional\":{\"show\":true,\"when\":\"individualOrEntity\",\"eq\":\"individual\"},\"type\":\"columns\",\"input\":false,\"tableView\":false,\"keyModified\":true},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"What account types / products are associated with this client? \",\"widget\":\"choicesjs\",\"tableView\":true,\"multiple\":true,\"data\":{\"values\":[{\"label\":\"Brokerage Account\",\"value\":\"brokerageAccount\"},{\"label\":\"Checking Account\",\"value\":\"checkingAccount\"},{\"label\":\"Collateral Account\",\"value\":\"collateralAccount\"},{\"label\":\"Custody Account\",\"value\":\"custodyAccount\"},{\"label\":\"Demand Deposit Account\",\"value\":\"demandDepositAccount\"},{\"label\":\"Fiduciary Account\",\"value\":\"fiduciaryAccount\"}]},\"validate\":{\"required\":true,\"multiple\":true},\"key\":\"clientAccountTypes\",\"type\":\"select\",\"input\":true},{\"label\":\"Select Wealth Management Product Booking Locations\",\"widget\":\"choicesjs\",\"tableView\":true,\"data\":{\"values\":[{\"label\":\"Brussels, Belgium\",\"value\":\"brusselsBelgium\"},{\"label\":\"Frankfurt, Germany\",\"value\":\"frankfurtGermany\"},{\"label\":\"Hong Kong\",\"value\":\"hongKong\"},{\"label\":\"London, UK\",\"value\":\"londonUk\"},{\"label\":\"Luxembourg\",\"value\":\"luxembourg\"},{\"label\":\"Mexico\",\"value\":\"mexico\"},{\"label\":\"USA\",\"value\":\"usa\"}]},\"validate\":{\"required\":true},\"key\":\"wmBookingLocations\",\"customConditional\":\"show = (data.customerEntityType == 'operatingCompany')\",\"type\":\"select\",\"input\":true}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"key\":\"columns30\",\"type\":\"columns\",\"input\":false,\"tableView\":false}],\"width\":8,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":8},{\"components\":[],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4}],\"key\":\"columns31\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}],\"key\":\"tabs\",\"type\":\"tabs\",\"input\":false,\"tableView\":false}],\"width\":12,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":12},{\"components\":[],\"width\":1,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":1}],\"key\":\"columns12\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}]}",
        "actionSchema": "{\"display\":\"form\",\"components\":[{\"label\":\"Submit\",\"action\":\"custom\",\"showValidations\":false,\"tableView\":false,\"key\":\"workflowButton_activity_0hbhsey\",\"type\":\"button\",\"input\":true,\"custom\":\"const workflowActionMapping = {};\\nconst postSubmitActionMapping ={\\n    postSubmitConfirmation:{\\n\\t     confirmationMessage: 'Ticket Submitted Successfully',\\n\\t     closeWindow:true\\n\\t}\\n}\\nObject.entries(component.properties).forEach((entry) => {\\n  const [key, value] = entry;\\n  workflowActionMapping[key] = value;\\n});\\ndata['workflowActionMapping'] = workflowActionMapping;\\ndata['postSubmitActionMapping'] = postSubmitActionMapping\\n\\ndata['COMPONENT_KEY'] = component['key'];\\ninstance.root.executeSubmit();\",\"disableOnInvalid\":true,\"tags\":[\"workflowAction\"],\"routingVariables\":{}}]}"
    },
    "formData": {
        "dateOfOrganization": "2009-12-01",
        "country": "United States Of America",
        "nonProfit": "yes",
        "clientFullName": "DAPPER REALTY GROUP LLC",
        "city": "BROOKLYN",
        "postalCode": "112358306",
        "countryOrganization": "United States Of America",
        "legalName": "DAPPER REALTY GROUP LLC",
        "stateDomicile": "New York",
        "addressLine1": "3000 OCEAN PKWY APT 3N",
        "state": "New York",
        "naicCode": "523940 - Portfolio Management And Investment Advice",
        "stateOrganization": "Delaware",
        "countryAssets": "United States Of America",
        "customerEntityType": "nbfi",
        "individualOrEntity": "entity",
        "countryDomicile": "United States Of America"
    }
}
