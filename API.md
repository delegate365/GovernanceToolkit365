# Governance Toolkit 365 API

These pages inform about how to use the Governance Toolkit 365 (GT365) and the API for various operations in Microsoft 365..

The GT365 API can be used from any other application or workflows. The API provides an HTTP endpoint that can be used with an HTTP POST request sending the required information, such as a valid token for the tenant and the payload. See the prerequesits and the required steps here.

## Prerequesits to use the API

1. You need to have a **Global Admin** of your Microsoft 365 tenant.
2. **Create an app** that is allowed to access the corresponding service method. Confirm the app permissions as Global Admin. This process is described at [API-Create-App](./API-create-app.md).
3. For **testing** and to follow the steps here, we recommend to use [Graph Explorer](http://aka.ms/ge), [Postman](https://www.getpostman.com/downloads/), or [CURL](https://curl.haxx.se/windows/), or create an Azure Logic App or a Microsoft Flow to communicate with the API. See the How-To below.
4. Call the API for every group to create with the required data. Use the method and the exact payload as below. Follow the links below.

## Functionality

Currently, the GT 365 API supports the following use cases:

| Method | Purpose |
|:----|:------|
| POST /api/InviteGuest | Invites a guest user to your Microsoft 365 tenant |
| POST /api/ProvisionTeam | Provisions a new Team with a Teams template |
| POST /api/ProvisionGroup | Provisions a new M365 group or a Team |
| POST /api/ArchiveTeam | Archives or unarchives an existing Team |
| POST /api/CloneTeam | Clones an existing Team into a new Team |

All methods must be called with the App credentials that allow GT365 to perform the operation. See the description and samples in this repository.

## Return codes

Each method returns a HTTP status code with a result.

| HTTP Statuscode | Description |
|:----|:------|
| 201 | Created. The operation was successful |
| 400 | Bad Request. A parameter is missing or is incorrect |
| 500 | Internal Server Error. The operation could not be completed |

If successful, the respective method returns a *HTTP Statuscode 201 Created* response. If data is missing or incorrect, a *HTTP 400 Bad Request* follows. If another error occurs, a Statuscode *HTTP 500 Internal Server Error* is returned.
The returned dataset returns a *message* that informs about the details of a failed operation.

### /api/InviteGuest

This method allows a user to invite another user with an external email address to their home tenant. Guests can attend meetings, view documents and chat in teams they're invited to. See the step-by-step description at [API-Invite-Guests](./API-invite-guest.md).

~~~~json
{
  "invitedUserDisplayName":"John Doe",
  "invitedUserEmailAddress": "john.doe@gmail.com",
  "inviteRedirectUrl": "https://mycompany.com/guestinfo",  
  "sendInvitationMessage": true,
  "requestedBy":"adele.vance@mycompany.com"
}
~~~~

**Note:** Provide a custom *inviteRedirectUrl* if needed. Otherwise, the default Microsoft redirect URL will be used.

### /api/ProvisionTeam

The ProvisionTeam method allows to provision a new Microsoft Team based on a given Microsoft Teams Template. 
If no templateId is provided, the standard Teams Template is used (as in the ProvisionGroup method).
See the step-by-step description at [API-Provision-Team](./API-provision-team.md).

~~~~json
{
    "displayName": "My Team 11",
    "mailNickname": "myteam11",
    "description": "This is my project team 11",
    "ownerUPNs": ["nestorw@M365x193702.onmicrosoft.com",
                  "biancap@M365x193702.onmicrosoft.com"],
    "memberUPNs": ["christiec@M365x193702.onmicrosoft.com",
                   "raulr@M365x193702.onmicrosoft.com"],    
    "visibility": "Private",
    "classification": "General",
    "templateId": "213e3d85-d45b-475e-8ae6-73baf497b18b"
}
~~~~

If you want to create a new team, we recommend to use this method.

**Note:** At least one *ownerUPN* email must be provided. If you do not want to add members in this step, provide an empty array: *"memberUPNs": []*. If no visibility is set, the Team will become a private Team. The *classification* can be an empty string "" or can be omitted.

### /api/ProvisionGroup

The ProvisionGroup method allows to provision a new Microsoft 365 group or a new Microsoft Team.
If no templateId is provided, the standard Teams Template is used (as in the ProvisionGroup method).
See the step-by-step description at [API-Provision-Team](./API-provision-team.md).

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
    "visibility": "Private",
    "classification": "General"
}
~~~~

**Note:** *createTeam* controls if just a new Microsoft 365 group shall be created, or a group that is team-ified. If set to *yes*, the team will be a team with the standard (empty) Teams template. At least one *ownerUPN* email must be provided. If you do not want to add any members in this step, provide an empty array: *"memberUPNs": []*. If no visibility is set, the Team will become a private group. The *classification* can be an empty string "" or can be omitted. 

### /api/ArchiveTeam

ArchiveTeam archives or unarchives an existing team. To identify the team to (un)archive, one key (email or displayName or teamId) is sufficient.
See the step-by-step description at [API-Archive-Team](./API-archive-team.md).

~~~~json
{
  "archive": true,
  "email": "myteam11@mytenant.onmicrosoft.com",
  "displayName": "My Team 11",
  "teamId":"04597f96-b754-4bd4-8e1e-c70c017f0324"
}
~~~~

**Note:** If *archive* ist set to *false*, an archived team will be restored. It can take a while until all content is restored, depending on the content of the team.

### /api/CloneTeam

Clones an existing team into a new team. This creates a copy of a team and you can specify which parts of the team to clone.
To identify the team to clone, one key (email or displayName or teamId) is sufficient.
See the step-by-step description at [API-Clone-Team](./API-clone-team.md).

~~~~json
{
  "archive": true,
  "email": "myteam11@mytenant.onmicrosoft.com",
  "displayName": "My Team 11",
  "teamId":"04597f96-b754-4bd4-8e1e-c70c017f0324",
  "apps": true,
  "channels": true,
  "members": true,
  "settings": true,
  "tabs": true
}
~~~~

More API calls are planned in the future. Feedback is welcome.
In case of questions, pls. contact us at [support@atwork.at](mailto:support@atwork.at?subject=GT365-API).

## Quick navigation

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provisioning](./API-provision-group.md) &middot; [API-Provisioning-Flow](./API-provision-group-flow.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)

