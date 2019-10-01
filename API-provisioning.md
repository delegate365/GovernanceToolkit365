# [Use the API](#use-the-api)

One you have [created the app](./API-create-app.md) in your Microsoft 365 tenant, we can use that app to access the GT365 API.

The security concept is to get a token for the own tenant first. Then send that token to the GT365 API, so that it is allowed to provision a new Office 365 group. The token usually is valid only for about 60 minutes and expires then.

As prerequesits, you need to have the app data from the step before, similar as here.
| Key | Value |
|:----|:------|
| AppID | 91eef8ad...
| AppSecret | /95=BRZ...
| TenantID | 21e6f8d3...


Use a tool to test the HTTP API requests. You can use any tool. This article here is using [Postman](https://www.getpostman.com/downloads/).

Follow the steps to provision a new Office 365 Group or Team.

- Postman allows to work with HTTP requests. After installing and opening the app, it looks empty as here.
[![link](./images/api-1.png)](./images/api-1.png "Click to enlarge")
- Fill in a **POST** request to get an access token with your app data. Find the documentation at [Get an access token](https://docs.microsoft.com/en-us/graph/auth-v2-service#4-get-an-access-token). Create a new HTTP POST request with the URI of https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
and add the key and value pairs with your own app data (the table you wrote down as above). We need to pass the **client_id, client_secret, scope** and the **grant_type** as a **application/x-www-form-urlencoded** formatted request as in the following graphics. Click "Send" when done.
[![link](./images/api-2.png)](./images/api-2.png "Click to enlarge")
- After sending the request, you get the **access_token** value for the request against the GT365 API. We need to pass that value in the Authorization header for the GT365 API call.
[![link](./images/api-3.png)](./images/api-3.png "Click to enlarge")
- Create a new request. This also is a **POST** request against the GT365 endpoint https://gt365api.atwork-it.com/api/ProvisionGroup. Copy the current **access_token** value in the Authorization Token field as shown here.
[![link](./images/api-4.png)](./images/api-4.png "Click to enlarge")
- Now, it´s time to add the payload for the API call. Submit a body in the following form, as shown in the screenshot. Click on "Body", add the JSON data (see below) and click "Send". You will see the result in the panel below.
[![link](./images/api-5.png)](./images/api-5.png "Click to enlarge")
Use this sample payload and adapt it as needed.

~~~~json
{
    "displayName": "My Group 10",
    "mailNickname": "mygroup10",
    "description": "This is my project group 10",
    "ownerUPNs": ["nestorw@M365x193702.onmicrosoft.com",
                  "biancap@M365x193702.onmicrosoft.com"],
    "memberUPNs": ["christiec@M365x193702.onmicrosoft.com",
                   "raulr@M365x193702.onmicrosoft.com"],    
    "createTeam": false,
    "visibility": "Private"
}
~~~~

Only these keys are mandatory: **displayName, mailNickname, ownerUPNs and visibility**.
The other keys can be provided if required. Usually, it makes sense to use the additional parameters to define the classification (that must be set in advance), and other group properties. 

Most keys are string. The following keys can have these predefined values.

|Key   |Value  |
|:-----|:------|
|createTeam | true&#124;false |
|visibility | Private&#124;Public |
|classification | Values must be set in the classification policy before they can be used as string here, e.g. "confidential" if set. See more [here](https://blog.atwork.at/post/2019/05/02/Groups-Governance-Toolkit-Policies). |

- The request can take from some seconds to 2 minutes, depending on the availability of the GT365 API. You will receive a HTTP status message after the operation has been completed.
- You get back a HTTP status code and a JSON message informing about the new group or any error message.

In case the provisioning was successful, you get back a result with a HTTP status code 201 as here.

~~~~json
{
    "version": {
        "major": 1,
        "minor": 1,
        "build": -1,
        "revision": -1,
        "majorRevision": -1,
        "minorRevision": -1
    },
    "content": {
        "headers": [
            {
                "key": "Content-Type",
                "value": [
                    "application/json; odata.metadata=minimal; odata.streaming=true; IEEE754Compatible=false; charset=utf-8"
                ]
            }
        ]
    },
    "statusCode": 201,
    "reasonPhrase": "Created",
    "headers": [
        {
            "key": "Cache-Control",
            "value": [
                "private"
            ]
        },
        {
            "key": "Transfer-Encoding",
            "value": [
                "chunked"
            ]
        },
        {
            "key": "Location",
            "value": [
                "https://graph.microsoft.com/v2/{TenantID}/directoryObjects/7058b418-4c15-49f7-b9b5-3630a16f4c75/Microsoft.DirectoryServices.Group"
            ]
        },
        {
            "key": "request-id",
            "value": [
                "82239735-900c-4d5a-bd08-1749b932e56e"
            ]
        },
        {
            "key": "client-request-id",
            "value": [
                "82239735-900c-4d5a-bd08-1749b932e56e"
            ]
        },
        {
            "key": "x-ms-ags-diagnostic",
            "value": [
                "{\"ServerInfo\":{\"DataCenter\":\"North Europe\",\"Slice\":\"SliceC\",\"Ring\":\"2\",\"ScaleUnit\":\"000\",\"RoleInstance\":\"AGSFE_IN_2\",\"ADSiteName\":\"NEU\"}}"
            ]
        },
        {
            "key": "OData-Version",
            "value": [
                "4.0"
            ]
        },
        {
            "key": "Duration",
            "value": [
                "440.8675"
            ]
        },
        {
            "key": "Strict-Transport-Security",
            "value": [
                "max-age=31536000"
            ]
        },
        {
            "key": "Date",
            "value": [
                "Tue, 01 Oct 2019 09:03:43 GMT"
            ]
        }
    ],
    "requestMessage": {
        "version": {
            "major": 2,
            "minor": 0,
            "build": -1,
            "revision": -1,
            "majorRevision": -1,
            "minorRevision": -1
        },
        "content": {
            "headers": [
                {
                    "key": "Content-Type",
                    "value": [
                        "application/json; charset=utf-8"
                    ]
                },
                {
                    "key": "Content-Length",
                    "value": [
                        "701"
                    ]
                }
            ]
        },
        "method": {
            "method": "POST"
        },
        "requestUri": "https://graph.microsoft.com/v1.0/groups",
        "headers": [
            {
                "key": "Authorization",
                "value": [
                    "Bearer {some-value}"
                ]
            },
            {
                "key": "Accept",
                "value": [
                    "application/json"
                ]
            },
            {
                "key": "Request-Context",
                "value": [
                    "appId=cid-v1:fcd32789-4a72-4362-ba23-a7598a41488a"
                ]
            },
            {
                "key": "traceparent",
                "value": [
                    "00-ea099a3f07555d4a8ede688e60b22a7d-5516a7ee0756d146-02"
                ]
            },
            {
                "key": "tracestate",
                "value": [
                    "az=cid-v1:fcd32789-4a72-4362-ba23-a7598a41488a"
                ]
            },
            {
                "key": "Request-Id",
                "value": [
                    "|ea099a3f07555d4a8ede688e60b22a7d.490f3e17_1."
                ]
            }
        ],
        "properties": {}
    },
    "isSuccessStatusCode": true
}
~~~~

The key "isSuccessStatusCode" with the value *true* can be used to see if the operation was successful or not.

- Check the created group or Team with Microsoft Graph, the Azure Portal or another mechanism. In this sample, the result looks as here. There are 2 group owners and in total 4 members (2 members plus the 2 owners).
[![link](./images/api-6.png)](./images/api-6.png "Click to enlarge")


## Error messages

If an error occurs during the operation, you get back a result with an "error" key as in the following samples.

If you send an invalid or expired token, the following message is returned.

~~~~json
{
  "error": {
    "code": "InvalidAuthenticationToken",
    "message": "CompactToken parsing failed with error code: 80049217",
    "innerError": {
      "request-id": "2f286794-6102-4009-9b50-300118150029",
      "date": "2019-10-01T07:19:34"
    }
  }
}
~~~~

If the request is mispelled or data is missing, you get a message, for example.

~~~~json
No visibility (Private|Public) was provided or had a wrong label.
~~~~

If the request sends data that cannot be set, you get a corresponding message. In this sample, a classification was sent, but the value ist not set in the policy of the tenant.

~~~~json
{
  "error": {
    "code": "Request_BadRequest",
    "message": "Property classification has an invalid value.",
    "innerError": {
      "request-id": "20567d85-74c6-49c8-a59a-5775863335f1",
      "date": "2019-10-01T07:22:13"
    },
    "details": [
      {
        "target": "classification",
        "code": "InvalidValue"
      }
    ]
  }
}
~~~~

If the request tries to create a group that is already existing, you get a message as here:

~~~~json
{
  "error": {
    "code": "Request_BadRequest",
    "message": "Another object with the same value for property mailNickname already exists.",
    "innerError": {
      "request-id": "decda332-fced-4983-be86-f01bda33175e",
      "date": "2019-10-01T07:16:35"
    },
    "details": [
      {
        "target": "mailNickname",
        "code": "ObjectConflict"
      }
    ]
  }
}
~~~~

If the request sends data that is not existing in the tenant, you get a message as here:

~~~~json
{
  "error": {
    "code": "InvalidRequest",
    "message": "Team owner not found for 5a6b746c-57eb-4d74-85c8-101af25d8b70.",
    "innerError": {
      "request-id": "3800e5a5-cc6c-4af0-b337-894d24025ab9",
      "date": "2019-10-01T07:40:21"
    }
  }
}
~~~~

In such cases, correct the data and retry.

## Use from any client

This sample shows the process how to use the GT365 API. You can test the API with Postman and then develop the API request from a Mirosoft Flow or Azure Logic App or from your own applications.
