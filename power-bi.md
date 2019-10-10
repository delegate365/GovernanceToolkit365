# Power BI

These pages inform about how to use the Governance Toolkit 365 (GT365) with Microsoft Power BI.

You can download the desktop client at the [Power BI website](https://powerbi.microsoft.com/en-us/downloads/). You can download a GT365 dashboard sample zip-file from [here](https://governancetoolkit365.com/download/GovernanceToolkit365-Template.zip).

We assume, the data for your tenant has already been generated, and you have got the Azure Storage Account name and key. You need that data to access your generated statistics.

## Connect to your data

Follow these steps to get your own data visualized in Power BI.

- Extract the zip file.
- Open the dashboard file GovernanceToolkit365-Template.pbit with your Power BI desktop client. When Power BO tries to update the content, an error can occur. If this message happens, simply click on "Close".
[![link](./images/powerbi-1.png)](./images/powerbi-1 "Click to enlarge")
- Now, let´s connect to your custom data source. Click on the "Edit queries" icon in the ribbon and select "data source settings".
[![link](./images/powerbi-2.png)](./images/powerbi-2 "Click to enlarge")
- Select the existing data source and click "Change Source..."
[![link](./images/powerbi-3.png)](./images/powerbi-3 "Click to enlarge")
- Copy the Azure Storage Account name into the "Account name or URL" field and click OK. You got en email with that data.
[![link](./images/powerbi-4.png)](./images/powerbi-4 "Click to enlarge")
- Wait till the box closes. You will see the new data source. Then, close box with "Close".
[![link](./images/powerbi-5.png)](./images/powerbi-5 "Click to enlarge")
- Confirm the changes with the "Apply changes" in the yellow message bar.
[![link](./images/powerbi-6.png)](./images/powerbi-6 "Click to enlarge")
- Now, Power BI will try to refresh the data. It will ask for the Storage Account key. Add that key and click "Connect".  You got en email with that data.
[![link](./images/powerbi-7.png)](./images/powerbi-7 "Click to enlarge")
- You should now see the to your own tenant data refreshed in the dashboards.
[![link](./images/powerbi-8.png)](./images/powerbi-8 "Click to enlarge")
- Save the file locally.
- Adapt the Power BI dashboard as needed and save any changes.
- Publish it the the Power BI portal to an Office 365 Group. Done.

Of course, you can create your own, custom Power BI dashboard from a blank Power BI file. Connect to your storage as described above.
  
## Samples

See some sample dashboards here: 

[![link](./images/bi-demo-1.png)](./images/bi-demo-1 "Click to enlarge")

[![link](./images/bi-demo-2.png)](./images/bi-demo-2 "Click to enlarge")

[![link](./images/bi-demo-3.png)](./images/bi-demo-3 "Click to enlarge")

[![link](./images/bi-demo-4.png)](./images/bi-demo-4 "Click to enlarge")

[![link](./images/bi-demo-5.png)](./images/bi-demo-5 "Click to enlarge")

[![link](./images/bi-demo-6.png)](./images/bi-demo-6 "Click to enlarge")


**Quick navigation**
[ReadMe](./readme.md) &middot; [API](./API.md) &middot; [API-Create-App](./API-create-app.md) &middot; [API-Provisioning](./API-provisioning.md) &middot; [API-Invite-Guests](./API-invite-guest.md) &middot; [Newsletter](./newsletter.md) &middot; [Power-BI](./power-bi.md) &middot; [GT365](https://governancetoolkit365.com/)
