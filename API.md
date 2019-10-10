# Governance Toolkit 365 API

These pages inform about how to use the Governance Toolkit 365 (GT365) and the API to provision a new Office 365 Group or Microsoft Team.

The GT365 API can be used from any other application or workflow. The API provides an HTTP endpoint that can be used with an HTTP POST request sending the required information, such as a valid token for the tenant and the group properties. See the prerequesits and the required steps here.

## Prerequesits

1. You need to have a **Global Admin** in your Office 365 tenant.
2. **Create an app** that is allowed to create a new group and confirm the app permissions as Global Admin. This process is described below.
4. For **testing** and to follow the steps here, we recommend to use [Graph Explorer](http://aka.ms/ge) or [Postman](https://www.getpostman.com/downloads/) or [CURL](https://curl.haxx.se/windows/), or create an Azure Logic App or a Microsoft Flow to communicate with the API. See the How-To below.

## Steps to use the API

Follow the steps below to setup the GT365 app.

1. Register an app in an one time process. Follow the steps at [Create an app](./API-create-app.md).
2. Call the API for every group to create with the required data. See the steps at [Use the API](./API-provisioning.md).

In case of questions, pls. contact us at [support@atwork.at](mailto:support@atwork.at?subject=GT365-API).

**Quick navigation**

[ReadMe](https://github.com/delegate365/GovernanceToolkit365/) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provisioning](./API-provisioning.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
