# [Clone team](#clone-team)

Once you have [created the app](./API-create-app.md) in your Microsoft 365 tenant, you can use that app to access the GT365 API.
Add the desired method below to the **[API base url](./API.md)**.

## /api/CloneTeam

This method allows to clone an existing team, with data you select. This creates a copy of a team and you can specify which parts of the team to clone.

This sample clones a team with the teamId 2e2b... into Team 13.

~~~~json
{
  "displayName": "Team 13",
  "email": "team13@mytenant.onmicrosoft.com",
  "teamId": "2e2b6dbb-83ae-49b5-9a98-e77ff1536eff",
  "apps": true,
  "channels": true,
  "members": true,
  "settings": true,
  "tabs": true
}
~~~~

**Note:** To identify the team to (un)archive, one key is sufficient: Submit an *email*, or the *DisplayName*, or the *teamId* for the team you want to archive. The following samples work as welland are equal to the first sample above.


**Note:** You can submit an *email*, or the *DisplayName* or the *teamId* for the team you want to clone.  
By default, all data are cloned, unless you specify a property you do not want to clone into the new team.

## Return codes

The method returns a status code for a successful operation: **HTTP 201 Created**.

~~~~json
{
  "teamId": "2e2b6dbb-83ae-49b5-9a98-e77ff1536eff",
  "message": "Successfully cloned Team Team12",
  "error": ""
}
~~~~

Any other status code means, the operation was not successful.  
If data is missing or is incorrect, a **HTTP 400 Bad Request** follows.  
If another error occurs, a Statuscode **HTTP 500 Internal Server Error** is returned.  
The returned dataset returns a *message* that informs about the details of a failed operation.  

Example: HTTP 400
Body:  
~~~~
Cannot clone. Missing parameters displayName, teamId, email - No display name provided No teamId provided No email provided 
~~~~

## Quick navigation

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provision-Team](./API-provision-team.md) &middot; [API-Provision-Group](./API-provision-group.md) &middot; [API-Provision-Group-Flow](./API-provision-group-flow.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
