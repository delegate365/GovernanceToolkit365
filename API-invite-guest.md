# [Invite guest](#invite-guest)

Once you have [created the app](./API-create-app.md) in your Microsoft 365 tenant, you can use that app to access the GT365 API.
Add the desired method below to the **[API base url](./API.md)**.

## /api/InviteGuest

This method allows a user to invite another user with an external email address to their home tenant. Guests can attend meetings, view documents and chat in teams they're invited to. See the step-by-step description at [API-Invite-Guests-Demo](./API-invite-guest-demo.md).

~~~~json
{
  "invitedUserDisplayName": "John Doe",
  "invitedUserEmailAddress": "john.doe@gmail.com",
  "inviteRedirectUrl": "https://mycompany.com/guestinfo",  
  "sendInvitationMessage": true,
  "requestedBy": "adele.vance@mycompany.com",
  "more": {
    "somecustomkey1": "some custom data1",
    "somecustomkey2": "some custom data2",
  }  
}
~~~~

**Note:** Provide a custom *inviteRedirectUrl* if needed. Otherwise, the default Microsoft redirect URL *https://invitations.microsoft.com* will be used.

The **more** key can be provided to store additional custom data. This key can contain up to 4000 characters in the classic key/value pairs shown above. This data is stored in the GT365 storage as a json object. If omitted, this field contains an empty {} expression.

## Return codes

The method returns a status code for a successful operation: **HTTP 201 Created**.

~~~~json
{
  "id": "<requestid>",
  "invitedUserEmailAddress": "john.doe@gmail.com",
  "inviteRedeemUrl": "https://login.microsoftonline.com/redeem?rd=https%3a%2f%2finvitations.microsoft.com%2fredeem%2f%3ftenant%3<tenantid>%26<userid>%26ticket%3d<ticketid>%3d2.0",
  "status": "PendingAcceptance",
  "sendInvitationMessage": true
}
~~~~

Any other status code means, the operation was not successful.  
If data is missing or is incorrect, a **HTTP 400 Bad Request** follows.  
If another error occurs, a Statuscode **HTTP 500 Internal Server Error** is returned.  
The returned dataset returns a *message* that informs about the details of a failed operation.  

## Quick navigation

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provision-Team](./API-provision-team.md) &middot; [API-Provision-Group](./API-provision-group.md) &middot; [API-Provision-Group-Flow](./API-provision-group-flow.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
