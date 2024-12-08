# .NET Blazor Server Webapp deployment demo
- **Author**:	Thomas Claudius Huber
- **Source code**: https://app.pluralsight.com/library/courses/blazor-server-application-ef-core-building-data-driven/

This repo uses given demo application to test .NET Blazor Server Webapp deployment.

# Deploy to Azure

## Create Azure App Service
1. Right-click project in VS 👉 Publish 👉 Azure 👉 Next 👉 Azure App Service (Linux) 👉 Next
2. Sign-in to your Microsoft subscription (if not yet) 👉 select your Azure subscription
3. Create new (App Service instance)
4. Set the following App Service settings:
   <br>👉 **Name:** WiredBrainCoffeeEmployeeManager-APP
   <br>👉 **Subscription name:** as selected (yours)
   <br>👉 **Resource group:** Pluralsight-RG
   <br>👉 **Hosting Plan:** WiredBrainCoffeeEmployeeManager-ASP, Poland Central, S1
6. Create 👉 wait until App Service instance gets created
7. Select created App Service instance 👉 Finish 👉 Close
8. In the Publish dialog set the following settings and 👉 Save
   <br>👉 **Configuration:** Release
   <br>👉 **Target Framework:** net8.0
   <br>👉 **Deployment Mode:** Self-contained
   <br>👉 **Target Runtime:** linux-x64
9. Right-click project in VS 👉 Publish 👉 Make sure it says "Ready to publish".
10. Scroll down 👉 notice that there is a serive dependecy 👉 SQL Server DB 👉 this has to be created first

## Setup Azure SQL Database
1. Right-click project in VS 👉 Publish 👉 Make sure it says "Ready to publish".
2. Scroll down 👉 notice that there is a serive dependecy 👉 SQL Server DB 👉 this has to be created first
3. Press "..." on the right 👉 Connect 👉 Azure SQL Database 👉 Next
4. Sign-in to your Microsoft subscription (if not yet) 👉 select your Azure subscription 👉 Create
5. In the dialog set the following settings:
   <br>👉 **Database name:** EmployeeManagerDb
   <br>👉 **Subscription name:** as selected (yours)
   <br>👉 **Resource group:** Pluralsight_RG
   <br>👉 Database server 👉 New ...
   <br>👉 **Database server name:** employeemanagerdbserver
   <br>👉 **Location:** Germany West Central
   <br>👉 **Administrator username:** ...
   <br>👉 **Administrator password:** ...
   <br>👉 OK 👉 Create
6. Wait until Azure SQL Database instance gets created 👉 Next
7. Provide connection string name and specify how to save it
   <br>👉 **Database connection string name:** ConnectionStrings:EmployeeManagerDbContext
   <br>👉 **Database connection user name:** as set in step #5
   <br>👉 **Database connection password:** as set in step #5
   <br>👉 **Save connection string value in:** Azure App Settings
   <br>👉 Copy **Connection string value** by pressing copy icon on the right
8. Next 👉 Finish 👉 wait until completed 👉 Close
9. Make sure that Azure SQL Database is marked as **Connected** with green checkmark

## Apply database migrations to Azure SQL Database
1. Open appsettings.json
2. Copy/paste line with EmployeeManagerDbContext connection string (have two same lines)
3. Comment out one of them.
4. Change the seconde one: paste connection string to Azure SQL DB as copied in step #7
5. Open Package Manager Console 👉  Update-Database
