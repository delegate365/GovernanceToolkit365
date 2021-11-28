# Governance Toolkit 365 API

These pages inform about how to use the Governance Toolkit 365 (GT365) and the API for various operations in Microsoft 365..

The GT365 API can be used from any other application or workflows. The API provides an HTTP endpoint that can be used with an HTTP POST request sending the required information, such as a valid token for the tenant and the payload. See the prerequesits and the required steps here.

## Prerequesits to use the API

1. You need to have a **Global Admin** of your Microsoft 365 tenant.
2. **Create an app** that is allowed to access the corresponding service method. Confirm the app permissions as Global Admin. This process is described at [API-Create-App](./API-create-app.md).
3. For **testing** and to follow the steps here, we recommend to use [Graph Explorer](http://aka.ms/ge), [Postman](https://www.getpostman.com/downloads/), or [CURL](https://curl.haxx.se/windows/), or create an Azure Logic App or a Microsoft Flow to communicate with the API. See the How-To below.
4. Call the API for every group to create with the required data. Use the method and the exact payload as below. Follow the links below.

## API base URL

Add the desired method to the **API base url** https://governancetoolkit365.azurewebsites.net
## Functionality

Currently, the GT 365 API supports the following use cases:

| Method | Purpose |
|:----|:------|
| [POST /api/InviteGuest](./) | Invites a guest user to your Microsoft 365 tenant |
| [POST /api/ProvisionTeam](./API-provision-team.md) | Provisions a new Team with a Teams template |
| [POST /api/ProvisionGroup](./) | Provisions a new M365 group or a Team |
| [POST /api/ArchiveTeam](./) | Archives or unarchives an existing Team |
| [POST /api/CloneTeam](./) | Clones an existing Team into a new Team |

All methods must be called with the App credentials that allow GT365 to perform the operation. See the description and samples in this repository.

## Return codes

Each method returns a HTTP status code with a result.

| HTTP Statuscode | Description |
|:----|:------|
| 201 | Created. The operation was successful |
| 400 | Bad Request. A parameter is missing or is incorrect |
| 500 | Internal Server Error. The operation could not be completed |

The method returns a status code for a successful operation: **HTTP 201 Created**.
Any other status code means, the operation was not successful.  
If data is missing or is incorrect, a **HTTP 400 Bad Request** follows.  
If another error occurs, a Statuscode **HTTP 500 Internal Server Error** is returned.  
The returned dataset returns a *message* that informs about the details of a failed operation.  

## Quick navigation

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provision-Team](./API-provision-team.md) &middot; [API-Provision-Group](./API-provision-group.md) &middot; [API-Provision-Group-Flow](./API-provision-group-flow.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
