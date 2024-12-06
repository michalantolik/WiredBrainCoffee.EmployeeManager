# .NET Blazor Server Webapp deployment demo
- **Author**:	Thomas Claudius Huber
- **Source code**: https://app.pluralsight.com/library/courses/blazor-server-application-ef-core-building-data-driven/

This repo uses given demo application to test .NET Blazor Server Webapp deployment.

# Deploy to Azure

## Create Azure App Service
1. Right-click project in VS 👉 Publish 👉 Azure 👉 Next 👉 Azure App Service (Linux) 👉 Next
2. Sign-in to your Microsoft subscription (if not yet) 👉 select your Azure subscription
3. Create new (App Service instance)
4. Set: Name, Subscription, Resource Group, Hosting Plan (e.g. S1 or S2) 👉 Create
5. Wait until App Service instance gets created.
6. Select created App Service instance 👉 Finish 👉 Close
7. In the Publish dialog set the following settings and close the dialog:
   <br>👉 Configuration: Release
   <br>👉 Target Framework: net8.0
   <br>👉 Deployment Mode: Self-contained
   <br>👉 Target Runtime: linux-x64
9. Right-click project in VS 👉 Publish 👉 Make sure it says "Ready to publish".
10. Scroll down 👉 notice that there is a serive dependecy 👉 SQL Server DB 👉 this has to be created first
