# [Use the API from Flow](#use-the-api)

Once you have [created the app](./API-create-app.md) in your Microsoft 365 tenant, we can use that app to access the GT365 API.

The security concept is to get a token for the own tenant first. Then send that token to the GT365 API, so that it is allowed to provision a new Office 365 group. The token usually is valid only for about 60 minutes and expires then.

As prerequesits, you need to have the app data from the step before, similar as here.
| Key | Value |
|:----|:------|
| AppID | 91eef8ad...
| AppSecret | /95=BRZ...
| TenantID | 21e6f8d3...


This document describes the basic steps when using the GT365 Provisioning API from Microsoft Flow.

Follow the steps to provision a new Office 365 Group or Team.

- Create a new Flow to test the GT365 API.
- The following screenshot shows an overview of the actions.
[![link](./images/api-provision-flow-1.png)](./images/api-provision-flow-1.png "Click to enlarge")
- Create a trigger to test your Flow. This can be a HTTP call, a newly added item to a SharePoint list or any other trigger. Here, we use a SPO list. Once a new item is added, the Flow starts.
[![link](./images/api-provision-flow-2.png)](./images/api-provision-flow-2.png "Click to enlarge")
- Add a new action "Initialize Variable", Use "AuthHeader" as name and leave the value empty.
[![link](./images/api-provision-flow-3.png)](./images/api-provision-flow-3.png "Click to enlarge")
- Add a new action "Initialize Variable", Use "AppID" as name and add your AppID from AAD as value.
[![link](./images/api-provision-flow-4.png)](./images/api-provision-flow-4.png "Click to enlarge")
- Add a new action "Compose".
[![link](./images/api-provision-flow-5.png)](./images/api-provision-flow-5.png "Click to enlarge")
- As "Inputs" value, add an expression with you App Secret, similiar as here. This ensures that any special characters in the secret are properly encoded. You can do that for all values if required.
~~~
encodeUriComponent('my[secret?code/12:34')
~~~
[![link](./images/api-provision-flow-6.png)](./images/api-provision-flow-6.png "Click to enlarge")

- Add a new action "HTTP" and configure it with an URI like here and add the variables from above. This step gets a token from Office 365 with the app data.
~~~
https://login.microsoftonline.com/variables('TenantID')/oauth2/v2.0/token?

Content-Type application/x-www-form-urlencoded

grant_type=client_credentials
&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default
&client_id=@{variables('AppID')}
&client_secret=@{outputs('Compose_Secret')}
~~~~
[![link](./images/api-provision-flow-8.png)](./images/api-provision-flow-8.png "Click to enlarge")

- Add a new action "Parse JSON" and add the Body from the GetToken action as "Content".
- Paste the following definition into the "Schema". This splits the keys and values from the previous step into usable properties.
~~~
{
    "type": "object",
    "properties": {
        "token_type": {
            "type": "string"
        },
        "expires_in": {
            "type": "integer"
        },
        "ext_expires_in": {
            "type": "integer"
        },
        "access_token": {
            "type": "string"
        }
    }
}
~~~

[![link](./images/api-provision-flow-9.png)](./images/api-provision-flow-9.png "Click to enlarge")

- Add a new action "Set Variable" and use "AuthHeader" as name. Add the string "Bearer" with a space and add the output from "Parse JSON" value.
~~~
Bearer @{body('Parse_JSON')?['access_token']}
~~~
[![link](./images/api-provision-flow-10.png)](./images/api-provision-flow-10.png "Click to enlarge")

- Add a new action "HTTP" and configure it with an URI like here:
- Create a HTTP POST action to the endpoint and add the Authorization and Content-Type as here:
~~~
https://gt365api.atwork-it.com/api/ProvisionGroup

Authorization @variables('AuthHeader')

Content-Type application/x-www-form-urlencoded
~~~

[![link](./images/api-provision-flow-11.png)](./images/api-provision-flow-11.png "Click to enlarge")

- Then, add the required parameters as here (filled from the SPO list or from other parameters).
~~~
{
  "displayName": "@{triggerBody()?['Title']}",
  "mailNickname": "@{triggerBody()?['Title']}",
  "description": "@{triggerBody()?['Title']}",
  "ownerUPNs": [
    "@{triggerBody()?['Author']?['Email']}"
  ],
  "memberUPNs": [
    "@{triggerBody()?['Author']?['Email']}"
  ],
  "createTeam": @{triggerBody()?['CreateTeam']},
  "visibility": "@{triggerBody()?['Visibility']?['Value']}"
}
~~~

- Done. Continue with other actions in your Flow.

## Test it

When the Flow is triggered, it should show an output similar as here.

[![link](./images/api-provision-flow-12.png)](./images/api-provision-flow-12.png "Click to enlarge")

The work is done in the ProvisionGroup action. The API returns a HTTP status code 201 and looks similar as here.

[![link](./images/api-provision-flow-13.png)](./images/api-provision-flow-13.png "Click to enlarge")
[![link](./images/api-provision-flow-14.png)](./images/api-provision-flow-14.png "Click to enlarge")

As Body, the new Group *id* and the *displayName* is returned.

## Integrate the Provisionging Flow in your Approval Workflow

A complete approval workflow could look like here.

[![link](./images/api-provision-flow-15.png)](./images/api-provision-flow-15.png "Click to enlarge")

If an error occured, the right branch is executed and the Flow terminates.

[![link](./images/api-provision-flow-16.png)](./images/api-provision-flow-16.png "Click to enlarge")

The condition branch provisions a group, if approved.

[![link](./images/api-provision-flow-17.png)](./images/api-provision-flow-17.png "Click to enlarge")

## Adapt it as needed

This sample shows the process how to use the GT365 API from Microsoft Flow or Microsoft Azure Logic Apps.


**Quick navigation**

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provisioning](./API-provisioning.md) &middot; [API-Provisioning-Flow](./API-provisioning-flow.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
