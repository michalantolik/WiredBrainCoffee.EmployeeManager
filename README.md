# .NET Blazor Server Webapp deployment demo

## Deployed application

https://wiredbraincoffeeemployeemanager-app.azurewebsites.net/

## This repository description

This repo uses given demo application to test .NET Blazor Server Webapp deployment.

Source code of the demo application can be found here:

https://app.pluralsight.com/library/courses/blazor-server-application-ef-core-building-data-driven/

... *by Thomas Claudius Huber*

## Deploy to Azure

### Create Azure App Service
1. Right-click project in VS 👉 Publish 👉 Azure 👉 Next 👉 Azure App Service (Linux) 👉 Next
2. Sign-in to your Microsoft subscription (if not yet) 👉 select your Azure subscription
3. Create new (App Service instance)
4. Set the following App Service settings:
   <br>👉 **Name:** WiredBrainCoffeeEmployeeManager-APP
   <br>👉 **Subscription name:** as selected (yours)
   <br>👉 **Resource group:** Pluralsight-RG
   <br>👉 **Hosting Plan:** WiredBrainCoffeeEmployeeManager-ASP, Canada Central, S1
6. Create 👉 wait until App Service instance gets created
7. Select created App Service instance 👉 Finish 👉 Close
8. In the Publish dialog set the following settings and 👉 Save
   <br>👉 **Configuration:** Release
   <br>👉 **Target Framework:** net8.0
   <br>👉 **Deployment Mode:** Self-contained
   <br>👉 **Target Runtime:** linux-x64
9. Right-click project in VS 👉 Publish 👉 Make sure it says "Ready to publish".
10. Scroll down 👉 notice that there is a serive dependecy 👉 SQL Server DB 👉 this has to be created first

### Setup Azure SQL Database
1. Right-click project in VS 👉 Publish 👉 Make sure it says "Ready to publish".
2. Scroll down 👉 notice that there is a serive dependecy 👉 SQL Server DB 👉 this has to be created first
3. Press "..." on the right 👉 Connect 👉 Azure SQL Database 👉 Next
4. Sign-in to your Microsoft subscription (if not yet) 👉 select your Azure subscription 👉 Create new (Azure SQL Database)
5. In the dialog set the following settings:
   <br>👉 **Database name:** WiredBrainCoffeeEmployeeManager-SQLDB
   <br>👉 **Subscription name:** as selected (yours)
   <br>👉 **Resource group:** Pluralsight-RG
   <br>👉 Database server 👉 New ...
   <br>👉 **Database server name:** employeemanager-sql
   <br>👉 **Location:** Canada Central
   <br>👉 **Administrator username:** ...
   <br>👉 **Administrator password:** ...
   <br>👉 OK 👉 Create
6. Wait until Azure SQL Database instance gets created 👉 Next
7. Provide connection string name and specify how to save it 👉 Azure App Settings
   <br>👉 **Database connection string name:** ConnectionStrings:EmployeeManagerDbContext
   <br>👉 **Database connection user name:** as set in step #5
   <br>👉 **Database connection password:** as set in step #5
   <br>👉 **Save connection string value in:** Azure App Settings
8. Next 👉 Finish 👉 wait until completed 👉 Close
9. Make sure that Azure SQL Database is marked as **Connected** with green checkmark

### Check Access to Azure SQL Database
1. Open Azure portal 👉 Open "WiredBrainCoffeeEmployeeManager-SQLDB" 👉 Query editor (preview)
2. Try to login using credentials given in step #5 👉 you should get error
   <br>👉 Cannot open server 'employeemanager-sql' requested by the login. Client with IP address 'xx.xx.x.xxx' is not allowed to access the server
4.  Overview 👉 Set server firewall 👉 Firewall rules 👉 Add your client IPv2 address (xx.xx.x.xxx) 👉 Save
5.  Open "WiredBrainCoffeeEmployeeManager-SQLDB" 👉 Query editor (preview)
6.  2. Login using credentials given in step #5 👉 it should work this time

### Apply database migrations to Azure SQL Database
1. Open Azure portal 👉 Open "WiredBrainCoffeeEmployeeManager-SQLDB" 👉 See connection strings
2. Copy "ADO.NET (SQL authentication)" connection string
3. Open appsettings.json
4. Copy/paste line with EmployeeManagerDbContext connection string (have two same lines)
5. Comment out one of them.
6. Change the seconde one: paste connection string to Azure SQL DB as copied in step #2
7. Replace {your_password} in connection string with the actual password.
8. Open Package Manager Console 👉  Update-Database
9. Open Azure portal 👉 Open "WiredBrainCoffeeEmployeeManager-SQLDB" 👉 Query editor (preview)
10. Login using your sql server credentials 👉 Tables 👉 Department and Employee tables should be there (migation was applied) 

## Publish the Application
1. Right-click project in VS 👉 Publish 👉 Publish button
2. Wait until application gets published
3. Browser will open the app automatically 👉 app (webstie) will be empty
4. VS will say "Warming up your site..." 👉 then VS will say "Publish succeeded on ..."
5. Wait a couple of mintes more...
6. Open Azure portal 👉 Open "WiredBrainCoffeeEmployeeManager-APP" 👉 Browse
7. Web browser will be open 👉 web application will be displayed
