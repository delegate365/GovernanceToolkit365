# [Provision Group](#provision-group)

Once you have [created the app](./API-create-app.md) in your Microsoft 365 tenant, you can use that app to access the GT365 API.
Add the desired method below to the **[API base url](./API.md)**.

[![link](./images/api-authentication.png)](./images/api-authentication.png "Click to enlarge")

## POST /api/ProvisionGroup

The ProvisionGroup method allows to provision a new Microsoft 365 group or a new Microsoft Team. 

Use this exact sample payload as the **body** and adjust it as needed:

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
    "createTeam": false
}
~~~~

**Note:** *createTeam* controls if just a new Microsoft 365 group shall be created, or a group that is team-ified. If set to *yes*, the team will be a team with the standard (empty) Teams template. At least one *ownerUPN* email must be provided. If you do not want to add any members in this step, provide an empty array: *"memberUPNs": []*. If no visibility is set, the Team will become a private group. The *classification* can be an empty string "" or can be omitted. 

## Specifications

- If you want to create a new team, we recommend to use this method.
- If no templateId is provided, the "standard" Teams Template is used (as in the ProvisionGroup method). The Standard Teams Template is the default (blank) template that is used, when a user creates a new, empty team.
- To get a teams templateId, see below.
- At least one *ownerUPN* email must be provided. 
- If you do not want to add members in this step, provide an empty array: *"memberUPNs": []*. 
- *visibility* can be *private* or *public*. If no visibility is set, the Team will become a private Team. 
- The *classification* can be an empty string "" or can be omitted.
- *createTeam* must be set to *true* or *false*, the default is false. If false, only a Microsoft 365 group is created without team. If set to true, a group and a team is created.
- The process usually takes at least 20 seconds, but can also take longer depending on the workload of the Microsoft 365 API.

## Samples

See some samples here.

### Sample 1 - Create a Microsoft 365 group

This is the minimal data that must be provided to create a new group (without a team).

~~~~json
{
  "displayName": "My Team 11",
  "mailNickname": "myteam11",
  "description": "This is my project team 11",
  "ownerUPNs": ["nestorw@M365x193702.onmicrosoft.com"],
  "memberUPNs": [ ],
  "createTeam": false
}
~~~~

### Sample 2 - Create a team

When createTeam is true, a new team is created. The standard Teams template is used. To create a (custom) predefined team, use [API-Provision-Team](./API-provision-team.md)

~~~~json
{
  "displayName": "My Team 12",
  "mailNickname": "myteam12",
  "description": "This is my project team 12",
  "ownerUPNs": ["nestorw@M365x193702.onmicrosoft.com",
                "biancap@M365x193702.onmicrosoft.com"],
  "memberUPNs": ["christiec@M365x193702.onmicrosoft.com"],    
  "visibility": "Public",
  "classification": "",
  "createTeam": true
}
~~~~

## Return codes

The method returns a status code for a successful operation: **HTTP 201 Created**.  
The return result is as follows. 

~~~~json
{
  "id": "b385f8dc-3487-4123-a7df-d62123effeb8",
  "displayName": "My Team 12",
  "type": "Group",
  "error": "",
  "message": "Team My Team 12 was successfully created."
}
~~~~

The *id* is the new group Id (that can be used for other operations).The  type is *Group* or *Team*. *error* includes any error message.

Any other status code means, the operation was not successful.  
If data is missing or is incorrect, a **HTTP 400 Bad Request** follows.  
If another error occurs, a Statuscode **HTTP 500 Internal Server Error** is returned.  
The returned dataset returns a *message* that informs about the details of a failed operation. 

## Quick navigation

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provision-Team](./API-provision-team.md) &middot; [API-Provision-Group](./API-provision-group.md) &middot; [API-Provision-Group-Flow](./API-provision-group-flow.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
