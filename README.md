{
    "traceId": "03e992079e40475c63f10e870175f369",
    "message": "Success",
    "config": {
        "bodySchema": "{\"display\":\"form\",\"components\":[{\"title\":\"Authorization Request\",\"collapsible\":false,\"key\":\"page1\",\"type\":\"panel\",\"label\":\"Page 1\",\"breadcrumbClickable\":true,\"buttonSettings\":{\"previous\":true,\"cancel\":true,\"next\":true},\"navigateOnEnter\":false,\"saveOnEnter\":false,\"scrollToTop\":false,\"input\":false,\"tableView\":false,\"components\":[{\"html\":\"<p style=\\\"margin-left:0px;\\\"><strong>Payment Authorization Disclaimer</strong></p><p style=\\\"margin-left:0px;\\\">By completing and submitting this form, you agree to the following terms:</p><ol><li><strong>Authorization</strong>: You authorize {{data?.clientIdentifiers?.trustName}} to process the payment as detailed in this form. This authorization is granted in accordance with the terms of the trust agreement.</li><li><strong>Purpose of Data Processing</strong>: Your personal data will be processed for the purpose of executing the payment from the trust. This processing is necessary for the performance of a contract to which you are a party.</li></ol><p style=\\\"margin-left:0px;\\\">By signing below, you confirm that you have read, understood, and agree to the terms outlined in this disclaimer.</p>\",\"label\":\"Content\",\"refreshOnChange\":false,\"key\":\"content\",\"type\":\"content\",\"input\":false,\"tableView\":false},{\"title\":\"<strong>Trust Details</strong>\",\"collapsible\":false,\"key\":\"panel4\",\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"content\":\"Trust Name</br><b>{{data?.clientIdentifiers?.trustName}}</b>\",\"refreshOnChange\":false,\"key\":\"html23\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false}],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4},{\"components\":[{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"content\":\"Trust Type</br><b>{{data?.clientIdentifiers?.trustType}}</b>\",\"refreshOnChange\":false,\"key\":\"html24\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false}],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4},{\"components\":[],\"size\":\"md\",\"width\":4,\"currentWidth\":4}],\"key\":\"columns8\",\"type\":\"columns\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"content\":\"Distribution Authority</br><b>{{data?.clientIdentifiers?.trustDispositionOmniCode}}</b>\",\"refreshOnChange\":false,\"key\":\"html25\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false}],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4},{\"components\":[{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"content\":\"Authorized Party</br><b>{{data?.clientIdentifiers?.trustDispositionOmniCode==='Discretionary'? \\\"J.P.Morgan\\\": data?.clientIdentifiers?.senderName}}</b>\",\"refreshOnChange\":false,\"key\":\"html26\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false}],\"width\":4,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":4},{\"components\":[{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"content\":\"Co-authorized Party</br>\",\"refreshOnChange\":false,\"key\":\"html27\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false}],\"size\":\"md\",\"width\":4,\"currentWidth\":4}],\"key\":\"columns9\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]},{\"title\":\"<strong>Summary</strong>\",\"collapsible\":false,\"key\":\"summaryPanel\",\"type\":\"panel\",\"label\":\"Panel\",\"input\":false,\"tableView\":false,\"components\":[{\"label\":\"Summary Text\",\"tag\":\"div\",\"attrs\":[{\"attr\":\"\",\"value\":\"\"}],\"content\":\"{{data.summaryText}}<br>\",\"refreshOnChange\":false,\"key\":\"summaryText\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false},{\"label\":\"Columns\",\"columns\":[{\"components\":[{\"label\":\"Key Information Identified\",\"disableAddingRemovingRows\":true,\"reorder\":false,\"addAnotherPosition\":\"bottom\",\"layoutFixed\":false,\"enableRowGroups\":false,\"initEmpty\":false,\"hideLabel\":true,\"tableView\":false,\"defaultValue\":[{\"eci\":\"\"}],\"key\":\"requestInformation\",\"customConditional\":\"show = !! data[\\\"requestInformation\\\"]\",\"type\":\"datagrid\",\"input\":true,\"components\":[{\"label\":\"Request Information\",\"columns\":[{\"components\":[{\"label\":\"HTML\",\"attrs\":[{\"attr\":\"style\",\"value\":\"text-align:left\"}],\"content\":\"{{row.desc}}: <b style=\\\"padding-left:5px\\\">{{row.value}}</b>\",\"refreshOnChange\":false,\"key\":\"html\",\"type\":\"htmlelement\",\"input\":false,\"tableView\":false}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"hideLabel\":true,\"key\":\"columns\",\"attributes\":{\"style\":\"text-align:left\"},\"type\":\"columns\",\"input\":false,\"tableView\":false}]}],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6},{\"components\":[],\"width\":6,\"offset\":0,\"push\":0,\"pull\":0,\"size\":\"md\",\"currentWidth\":6}],\"key\":\"columns7\",\"type\":\"columns\",\"input\":false,\"tableView\":false}]}]}]}",
        "actionSchema": "{\"display\":\"form\",\"components\":[{\"label\":\"Rejected\",\"action\":\"custom\",\"showValidations\":false,\"theme\":\"danger\",\"disableOnInvalid\":true,\"tableView\":false,\"key\":\"workflowButton_Activity_0eq8pthrejected\",\"tags\":[\"workflowAction\"],\"properties\":{\"clientAction\":\"Rejected\"},\"routingVariables\":{},\"type\":\"button\",\"custom\":\"const workflowActionMapping = {};\\nconst postSubmitActionMapping ={\\n    postSubmitConfirmation:{\\n\\t     confirmationMessage: 'Ticket Submitted Successfully',\\n\\t     closeWindow:true\\n\\t}\\n}\\nObject.entries(component.properties).forEach((entry) => {\\n  const [key, value] = entry;\\n  workflowActionMapping[key] = value;\\n});\\ndata['workflowActionMapping'] = workflowActionMapping;\\ndata['postSubmitActionMapping'] = postSubmitActionMapping\\n\\ndata['COMPONENT_KEY'] = component['key'];\\ninstance.root.executeSubmit();\",\"input\":true},{\"label\":\"Approved\",\"action\":\"custom\",\"showValidations\":false,\"tableView\":false,\"key\":\"workflowButton_Activity_0eq8pthapproved\",\"properties\":{\"clientAction\":\"Approved\"},\"type\":\"button\",\"input\":true,\"custom\":\"const workflowActionMapping = {};\\nconst postSubmitActionMapping ={\\n    postSubmitConfirmation:{\\n\\t     confirmationMessage: 'Ticket Submitted Successfully',\\n\\t     closeWindow:true\\n\\t}\\n}\\nObject.entries(component.properties).forEach((entry) => {\\n  const [key, value] = entry;\\n  workflowActionMapping[key] = value;\\n});\\ndata['workflowActionMapping'] = workflowActionMapping;\\ndata['postSubmitActionMapping'] = postSubmitActionMapping\\n\\ndata['COMPONENT_KEY'] = component['key'];\\ninstance.root.executeSubmit();\",\"disableOnInvalid\":true,\"tags\":[\"workflowAction\"]}]}"
    },
    "formData": {
        "ticketNumber": "",
        "feedbackContainer": {
            "additionalComments": "",
            "submitFeedback": false,
            "pleaseProvideYourFeedbackOnTheAiGeneratedSummaryAndActionItems": ""
        },
        "applicationType": "BSR",
        "emailBody": "\n    <div>\n      <div><html xmlns:v=\"urn:schemas-microsoft-com:vml\" xmlns:o=\"urn:schemas-microsoft-com:office:office\" xmlns:w=\"urn:schemas-microsoft-com:office:word\" xmlns:m=\"http://schemas.microsoft.com/office/2004/12/omml\" xmlns=\"http://www.w3.org/TR/REC-html40\"><head><meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\"><meta name=\"Generator\" content=\"Microsoft Word 15 (filtered medium)\"><style><!--\n/* Font Definitions */\n@font-face\n\t{font-family:\"Cambria Math\";\n\tpanose-1:2 4 5 3 5 4 6 3 2 4;}\n@font-face\n\t{font-family:Calibri;\n\tpanose-1:2 15 5 2 2 2 4 3 2 4;}\n@font-face\n\t{font-family:Aptos;}\n/* Style Definitions */\np.MsoNormal, li.MsoNormal, div.MsoNormal\n\t{margin:0in;\n\tfont-size:11.0pt;\n\tfont-family:\"Aptos\",sans-serif;}\np.MsoPlainText, li.MsoPlainText, div.MsoPlainText\n\t{mso-style-priority:99;\n\tmso-style-link:\"Plain Text Char\";\n\tmargin:0in;\n\tfont-size:11.0pt;\n\tfont-family:\"Calibri\",sans-serif;}\nspan.EmailStyle17\n\t{mso-style-type:personal-compose;\n\tfont-family:\"Aptos\",sans-serif;\n\tcolor:windowtext;}\nspan.PlainTextChar\n\t{mso-style-name:\"Plain Text Char\";\n\tmso-style-priority:99;\n\tmso-style-link:\"Plain Text\";\n\tfont-family:\"Calibri\",sans-serif;}\n.MsoChpDefault\n\t{mso-style-type:export-only;\n\tfont-size:11.0pt;\n\tmso-ligatures:none;}\n@page WordSection1\n\t{size:8.5in 11.0in;\n\tmargin:1.0in 1.0in 1.0in 1.0in;}\ndiv.WordSection1\n\t{page:WordSection1;}\n--></style><!--[if gte mso 9]><xml><o:shapedefaults v:ext=\"edit\" spidmax=\"1026\" /></xml><![endif]--><!--[if gte mso 9]><xml><o:shapelayout v:ext=\"edit\"><o:idmap v:ext=\"edit\" data=\"1\" /></o:shapelayout></xml><![endif]--></head><body lang=\"EN-US\" link=\"#467886\" vlink=\"#96607D\" style=\"word-wrap:break-word\"><div class=\"WordSection1\"><p class=\"MsoPlainText\">Ashley,<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">I hope this message finds you well. I am reaching out to request the release of funds to cover medical expenses, travel, and other essential costs associated with my upcoming surgery on July 9th. &nbsp;We require a total of $104,000, and\n a prompt disbursement of these funds to my JP Morgan account M58746005 would be immensely appreciated.&nbsp; I’m attaching here the bills supporting my request.<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">Your understanding and support during this critical time would greatly alleviate our concerns and allow us to focus on my health and recovery.<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">Thank you very much for considering my request. I look forward to your timely response.<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">Jayson<o:p></o:p></p><p class=\"MsoNormal\"><o:p>&nbsp;</o:p></p></div></body></html></div>\n    </div>\n  ",
        "documents": [
            {
                "docPackSequence": 1,
                "autoApprovedOnUpload": true,
                "code": "051",
                "documentLevel": "PROCESS",
                "name": "Supporting Document",
                "documentCategory": "Internal"
            }
        ],
        "conversations": [
            {
                "conversationId": "AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=",
                "mailboxName": "awmcctask.management.four@jpmorgan.com"
            }
        ],
        "viewTrustDocuments1": false,
        "mailboxName": "awmcctask.management.four@jpmorgan.com",
        "distInfoToAccountValue": "M58746005",
        "requestInformation": [
            {
                "context": "",
                "value": "Jayson Lashin",
                "key": "Requestor's Name",
                "desc": " Requestor's  Name"
            },
            {
                "context": "",
                "value": "AWMCCTask Management Four",
                "key": "Recipient's Name",
                "desc": " Recipient's  Name"
            },
            {
                "context": "",
                "value": "awmcctask.management.four@jpmorgan.com",
                "key": "Recipient's Email Address",
                "desc": " Recipient's  Email  Address"
            },
            {
                "context": "",
                "value": "$104,000",
                "key": "Requested Amount",
                "desc": " Requested  Amount"
            },
            {
                "context": "",
                "value": "Jayson Lashin",
                "key": "Beneficiary",
                "desc": " Beneficiary"
            },
            {
                "context": "",
                "value": "Medical/RX/Counseling/Therapy/Hospitalization",
                "key": "Purpose Category",
                "desc": " Purpose  Category"
            },
            {
                "context": "",
                "value": "Cover medical expenses, travel, and other essential costs for surgery",
                "key": "Purpose of Distribution",
                "desc": " Purpose of  Distribution"
            },
            {
                "context": "",
                "value": "M58746005",
                "key": "Account Number(s)",
                "desc": " Account  Number(s)"
            },
            {
                "context": "",
                "value": "Upcoming surgery on July 9th",
                "key": "Deadline or urgency",
                "desc": " Deadline or urgency"
            },
            {
                "context": "",
                "value": "bills supporting request",
                "key": "Attachments",
                "desc": " Attachments"
            },
            {
                "context": "",
                "value": "Your understanding and support during this critical time would greatly alleviate our concerns and allow us to focus on my health and recovery.",
                "key": "Supporting details",
                "desc": " Supporting details"
            }
        ],
        "email": {
            "date": "6/6/2025, 4:58:06 PM",
            "attachments": [
                {
                    "s3KeyPath": "awmcctask.management.four@jpmorgan.com/AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=/<SJ0P130MB0211C14E6B989A7634587793886EA@SJ0P130MB0211.NAMP130.PROD.OUTLOOK.COM>/AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAxoTCCaPzX06z98unMKj1cQ==/DAR Sample 1.pdf",
                    "size": 0,
                    "emailReceivedDate": "2025-06-06T20:58:06.000Z",
                    "attachmentCategory": "EXTERNAL",
                    "name": "DAR Sample 1.pdf",
                    "uploadStatus": "SUCCESS",
                    "id": "AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAxoTCCaPzX06z98unMKj1cQ==",
                    "mimeType": "application/pdf"
                },
                {
                    "s3KeyPath": "awmcctask.management.four@jpmorgan.com/AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=/<SJ0P130MB0211C14E6B989A7634587793886EA@SJ0P130MB0211.NAMP130.PROD.OUTLOOK.COM>/AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAOS2umzTuRUSYroeRfjpDYg==/DAR Sample 2.pdf",
                    "size": 0,
                    "emailReceivedDate": "2025-06-06T20:58:06.000Z",
                    "attachmentCategory": "EXTERNAL",
                    "name": "DAR Sample 2.pdf",
                    "uploadStatus": "SUCCESS",
                    "id": "AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAOS2umzTuRUSYroeRfjpDYg==",
                    "mimeType": "application/pdf"
                }
            ],
            "emailBody": "\n    <div>\n      <div><html xmlns:v=\"urn:schemas-microsoft-com:vml\" xmlns:o=\"urn:schemas-microsoft-com:office:office\" xmlns:w=\"urn:schemas-microsoft-com:office:word\" xmlns:m=\"http://schemas.microsoft.com/office/2004/12/omml\" xmlns=\"http://www.w3.org/TR/REC-html40\"><head><meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\"><meta name=\"Generator\" content=\"Microsoft Word 15 (filtered medium)\"><style><!--\n/* Font Definitions */\n@font-face\n\t{font-family:\"Cambria Math\";\n\tpanose-1:2 4 5 3 5 4 6 3 2 4;}\n@font-face\n\t{font-family:Calibri;\n\tpanose-1:2 15 5 2 2 2 4 3 2 4;}\n@font-face\n\t{font-family:Aptos;}\n/* Style Definitions */\np.MsoNormal, li.MsoNormal, div.MsoNormal\n\t{margin:0in;\n\tfont-size:11.0pt;\n\tfont-family:\"Aptos\",sans-serif;}\np.MsoPlainText, li.MsoPlainText, div.MsoPlainText\n\t{mso-style-priority:99;\n\tmso-style-link:\"Plain Text Char\";\n\tmargin:0in;\n\tfont-size:11.0pt;\n\tfont-family:\"Calibri\",sans-serif;}\nspan.EmailStyle17\n\t{mso-style-type:personal-compose;\n\tfont-family:\"Aptos\",sans-serif;\n\tcolor:windowtext;}\nspan.PlainTextChar\n\t{mso-style-name:\"Plain Text Char\";\n\tmso-style-priority:99;\n\tmso-style-link:\"Plain Text\";\n\tfont-family:\"Calibri\",sans-serif;}\n.MsoChpDefault\n\t{mso-style-type:export-only;\n\tfont-size:11.0pt;\n\tmso-ligatures:none;}\n@page WordSection1\n\t{size:8.5in 11.0in;\n\tmargin:1.0in 1.0in 1.0in 1.0in;}\ndiv.WordSection1\n\t{page:WordSection1;}\n--></style><!--[if gte mso 9]><xml><o:shapedefaults v:ext=\"edit\" spidmax=\"1026\" /></xml><![endif]--><!--[if gte mso 9]><xml><o:shapelayout v:ext=\"edit\"><o:idmap v:ext=\"edit\" data=\"1\" /></o:shapelayout></xml><![endif]--></head><body lang=\"EN-US\" link=\"#467886\" vlink=\"#96607D\" style=\"word-wrap:break-word\"><div class=\"WordSection1\"><p class=\"MsoPlainText\">Ashley,<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">I hope this message finds you well. I am reaching out to request the release of funds to cover medical expenses, travel, and other essential costs associated with my upcoming surgery on July 9th. &nbsp;We require a total of $104,000, and\n a prompt disbursement of these funds to my JP Morgan account M58746005 would be immensely appreciated.&nbsp; I’m attaching here the bills supporting my request.<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">Your understanding and support during this critical time would greatly alleviate our concerns and allow us to focus on my health and recovery.<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">Thank you very much for considering my request. I look forward to your timely response.<o:p></o:p></p><p class=\"MsoPlainText\"><o:p>&nbsp;</o:p></p><p class=\"MsoPlainText\">Jayson<o:p></o:p></p><p class=\"MsoNormal\"><o:p>&nbsp;</o:p></p></div></body></html></div>\n    </div>\n  ",
            "subject": "Request For Distribution",
            "from": {
                "emailAddress": "jayson.lashin@jpmorgan.com",
                "name": "Lashin, Jayson (WM, USA)"
            },
            "to": [
                {
                    "emailAddress": "awmcctask.management.four@jpmorgan.com",
                    "name": "AWMCCTask Management Four"
                }
            ]
        },
        "summaryResponse": {
            "requestAction": "createTicket",
            "requestSummary": "Funds for surgery",
            "requestOverview": "Request for funds for medical expenses and surgery.",
            "intentType": "Distribution",
            "intentSummary": "Request for $104,000 to cover medical expenses, travel, and other essential costs for upcoming surgery on July 9th.",
            "intentConfidence": "95",
            "intentConfidenceReason": "The email explicitly requests funds for medical expenses and provides a specific amount and account number.",
            "senderInfo": {
                "emailAddress": "jayson.lashin@jpmorgan.com",
                "identifiers": {
                    "accountNumber": "P17879001",
                    "accountStatusCode": "OPE",
                    "partyAcctRelTypeCode": "IP",
                    "partyECIId": "0767180771",
                    "partyRoleName": "Beneficiary",
                    "primaryOwnerIndicator": "N",
                    "party": {
                        "clientPhoneEmails": [
                            {
                                "preferredAddressIndicator": "N",
                                "unconvertedPhoneNumber": "5163128799",
                                "emailAddress": "jayson.lashin@jpmorgan.com",
                                "unformattedPhoneNumber": "5163128799",
                                "formattedPhoneNumberAddress": "5163128799",
                                "internationalDiallingCode": "+1",
                                "phoneExtensionAddress": "123"
                            }
                        ],
                        "clntFullName": "Lashin, Jayson",
                        "firstName": "Jayson",
                        "lastName": ""
                    },
                    "linkedTrusts": [
                        {
                            "senderRoles": [
                                "Beneficiary"
                            ],
                            "partyRoleName": "Sole Owner",
                            "distributionProvisionTypeName": "INC, PRIN DISC",
                            "accountNumber": "P17879001",
                            "partyECIId": "0221129834",
                            "party": {
                                "clntFullName": "BANYAN FINANCIAL SERVICES LLC",
                                "clientEmployees": [
                                    {
                                        "employeeStandardEmailAddress": "nannette.fridley@jpmorgan.com",
                                        "employeeFullName": "Nannette O Fridley",
                                        "teamMemberRoleName": "Secondary T&E Officer",
                                        "employeeStandardIdentifier": "U039082"
                                    },
                                    {
                                        "employeeStandardEmailAddress": "noreen.gawley@jpmorgan.com",
                                        "employeeFullName": "Noreen A Gawley",
                                        "teamMemberRoleName": "T&E Professional",
                                        "employeeStandardIdentifier": "N040504"
                                    },
                                    {
                                        "employeeStandardEmailAddress": "heli.patel@jpmorgan.com",
                                        "employeeFullName": "Heli R Patel",
                                        "teamMemberRoleName": "Secondary T&E Professional",
                                        "employeeStandardIdentifier": "V785781"
                                    },
                                    {
                                        "employeeStandardEmailAddress": "jayson.lashin@jpmorgan.com",
                                        "employeeFullName": "Jayson Lashin",
                                        "teamMemberRoleName": "T&E Officer",
                                        "employeeStandardIdentifier": "O485210"
                                    },
                                    {
                                        "employeeStandardEmailAddress": "jennifer.c.tigani@jpmorgan.com",
                                        "employeeFullName": "Jennifer C Tigani",
                                        "teamMemberRoleName": "T&E Administrator",
                                        "employeeStandardIdentifier": "N103420"
                                    }
                                ]
                            }
                        }
                    ]
                }
            },
            "clientECI": "0767180771",
            "clientIdentifiers": {
                "comparison_list": [
                    {
                        "is_match": true,
                        "matched_confidence_reason": "Exact match found for 'Jayson Lashin' in clientEmployees with matching email address.",
                        "identifiers": [
                            {
                                "value": "Jayson Lashin",
                                "key": "employeeFullName"
                            },
                            {
                                "value": "T&E Officer",
                                "key": "teamMemberRoleName"
                            },
                            {
                                "value": "O485210",
                                "key": "employeeStandardIdentifier"
                            },
                            {
                                "value": "jayson.lashin@jpmorgan.com",
                                "key": "employeeStandardEmailAddress"
                            }
                        ],
                        "source": {
                            "value": "Jayson Lashin",
                            "key": "clientEmployees"
                        },
                        "extracted": {
                            "value": "Jayson Lashin",
                            "key": "Requestor's Name"
                        },
                        "matched_confidence": 0.95
                    },
                    {
                        "is_match": true,
                        "matched_confidence_reason": "Partial match found for 'Jayson Lashin' as 'Lashin, Jayson' in party with matching email address.",
                        "identifiers": [
                            {
                                "value": "0767180771",
                                "key": "partyECIId"
                            },
                            {
                                "value": "P17879001",
                                "key": "accountNumber"
                            },
                            {
                                "value": "Lashin, Jayson",
                                "key": "clntFullName"
                            },
                            {
                                "value": "jayson.lashin@jpmorgan.com",
                                "key": "emailAddress"
                            }
                        ],
                        "source": {
                            "value": "Lashin, Jayson",
                            "key": "party"
                        },
                        "extracted": {
                            "value": "Jayson Lashin",
                            "key": "Beneficiary"
                        },
                        "matched_confidence": 0.9
                    },
                    {
                        "is_match": false,
                        "matched_confidence_reason": "No direct match found for 'AWMCCTask Management Four'. Possible role-related match with 'Secondary T&E Officer'.",
                        "identifiers": [
                            {
                                "value": "Nannette O Fridley",
                                "key": "employeeFullName"
                            },
                            {
                                "value": "Secondary T&E Officer",
                                "key": "teamMemberRoleName"
                            },
                            {
                                "value": "U039082",
                                "key": "employeeStandardIdentifier"
                            },
                            {
                                "value": "nannette.fridley@jpmorgan.com",
                                "key": "employeeStandardEmailAddress"
                            }
                        ],
                        "source": {
                            "value": "Nannette O Fridley",
                            "key": "clientEmployees"
                        },
                        "extracted": {
                            "value": "AWMCCTask Management Four",
                            "key": "Recipient's Name"
                        },
                        "matched_confidence": 0.3
                    },
                    {
                        "is_match": false,
                        "matched_confidence_reason": "No match found for 'awmcctask.management.four@jpmorgan.com'.",
                        "identifiers": [
                            {
                                "value": "Nannette O Fridley",
                                "key": "employeeFullName"
                            },
                            {
                                "value": "Secondary T&E Officer",
                                "key": "teamMemberRoleName"
                            },
                            {
                                "value": "U039082",
                                "key": "employeeStandardIdentifier"
                            },
                            {
                                "value": "nannette.fridley@jpmorgan.com",
                                "key": "employeeStandardEmailAddress"
                            }
                        ],
                        "source": {
                            "value": "nannette.fridley@jpmorgan.com",
                            "key": "clientEmployees"
                        },
                        "extracted": {
                            "value": "awmcctask.management.four@jpmorgan.com",
                            "key": "Recipient's Email Address"
                        },
                        "matched_confidence": 0.2
                    }
                ]
            },
            "requestInformation": [
                {
                    "context": "",
                    "value": "Jayson Lashin",
                    "key": "Requestor's Name"
                },
                {
                    "context": "",
                    "value": "AWMCCTask Management Four",
                    "key": "Recipient's Name"
                },
                {
                    "context": "",
                    "value": "awmcctask.management.four@jpmorgan.com",
                    "key": "Recipient's Email Address"
                },
                {
                    "context": "",
                    "value": "$104,000",
                    "key": "Requested Amount"
                },
                {
                    "context": "",
                    "value": "Jayson Lashin",
                    "key": "Beneficiary"
                },
                {
                    "context": "",
                    "value": "Medical/RX/Counseling/Therapy/Hospitalization",
                    "key": "Purpose Category"
                },
                {
                    "context": "",
                    "value": "Cover medical expenses, travel, and other essential costs for surgery",
                    "key": "Purpose of Distribution"
                },
                {
                    "context": "",
                    "value": "M58746005",
                    "key": "Account Number(s)"
                },
                {
                    "context": "",
                    "value": "Upcoming surgery on July 9th",
                    "key": "Deadline or urgency"
                },
                {
                    "context": "",
                    "value": "bills supporting request",
                    "key": "Attachments"
                },
                {
                    "context": "",
                    "value": "Your understanding and support during this critical time would greatly alleviate our concerns and allow us to focus on my health and recovery.",
                    "key": "Supporting details"
                }
            ]
        },
        "conversationId": "AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=",
        "intentId": "AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=",
        "distInfoFromAccountValue": "P17879001",
        "attributes": {
            "initiatorSid": "K005958",
            "processStatus": "",
            "hierarchyId": "5396222",
            "largeClient": "N",
            "eci": "0767180771",
            "owningTeamCode": "PB_FID_DEL_BLUE",
            "sugarCaseId": "",
            "categoryDesc": "Trust",
            "activityId": "7987c9d4-4569-11f0-9cb4-1257f8c16705",
            "requestSubTypeDesc": "Client & Account",
            "activityDisplayName": "Trust Officer Verification",
            "ownerName": "Ashley L Slutter",
            "processId": "72c39c6a-4569-11f0-9227-128fbd0a548f",
            "assigneeName": "Ashley L Slutter",
            "caseId": "96001247122",
            "activityTypeCode": "Activity_0ya9jne",
            "activityStatus": "New",
            "gwmId": "U0004046482",
            "requestTypeDesc": "Client Requests",
            "formId": "tECase-185-Activity_0ya9jne-WORKFLOW",
            "processDefinitionId": "tECase",
            "entityCode": "USA",
            "owningTeamName": "PB FID DELAWARE BLUE",
            "assigneeSid": "R511010",
            "accountNumber": "",
            "env": "pbatest",
            "pageFrom": "Service_Blotter",
            "loggedInUserSid": "R511010",
            "taskStartDate": "09 Jun 2025 3:39 PM",
            "ownerSid": "R511010",
            "processDefinitionVersion": "185",
            "businessSystemCode": ""
        },
        "emailAttachments": [
            {
                "s3KeyPath": "awmcctask.management.four@jpmorgan.com/AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=/<SJ0P130MB0211C14E6B989A7634587793886EA@SJ0P130MB0211.NAMP130.PROD.OUTLOOK.COM>/AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAxoTCCaPzX06z98unMKj1cQ==/DAR Sample 1.pdf",
                "size": 0,
                "emailReceivedDate": "2025-06-06T20:58:06.000Z",
                "attachmentCategory": "EXTERNAL",
                "name": "DAR Sample 1.pdf",
                "uploadStatus": "SUCCESS",
                "id": "AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAxoTCCaPzX06z98unMKj1cQ==",
                "mimeType": "application/pdf"
            },
            {
                "s3KeyPath": "awmcctask.management.four@jpmorgan.com/AAQkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUwM2I2ZWVlZQAQABrC1KdIWEeqnhLQXKKi5Ro=/<SJ0P130MB0211C14E6B989A7634587793886EA@SJ0P130MB0211.NAMP130.PROD.OUTLOOK.COM>/AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAOS2umzTuRUSYroeRfjpDYg==/DAR Sample 2.pdf",
                "size": 0,
                "emailReceivedDate": "2025-06-06T20:58:06.000Z",
                "attachmentCategory": "EXTERNAL",
                "name": "DAR Sample 2.pdf",
                "uploadStatus": "SUCCESS",
                "id": "AQMkADA3MWRjZDRmLWMwN2ItNDU2My1hZDg2LWNhNTUAMDNiNmVlAgBGAAADIRmD8wxkBkuKqOgbVLAbXQcAbgTbSMy6ZEax/GwWV8wHSgAAAgEMAAAADout/3UXD0a7tx35tqNmdAACc3ffZQAAAAESABAAOS2umzTuRUSYroeRfjpDYg==",
                "mimeType": "application/pdf"
            }
        ],
        "distInfoAmountValue": "$104,000",
        "docSetId": "dd7495ce-6fad-4333-99c3-8cab442bdb1a"
    }
}
