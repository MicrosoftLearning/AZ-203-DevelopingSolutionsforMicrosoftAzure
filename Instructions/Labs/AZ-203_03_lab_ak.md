---
lab:
    title: 'Lab: Constructing a polyglot data solution'
    type: 'Answer Key'
    module: 'AZ-203T03-A: Develop for Azure Storage'
---

# Lab: Constructing a polyglot data solution
# Student lab answer key

## Microsoft Azure user interface

Given the dynamic nature of Microsoft cloud tools, you might experience Azure user interface (UI) changes following the development of this training content. These changes might cause the lab instructions and steps to not match up correctly.

Microsoft updates this training course as soon as the community brings needed changes to our attention. However, because cloud updates occur frequently, you might encounter UI changes before this training content is updated. **If this occurs, adapt to the changes and work through them in the labs as needed.**

## Instructions

### Before you start

#### Sign in to the lab virtual machine

Sign in to your **Windows 10** virtual machine using the following credentials:

-   **Username**: Admin

-   **Password**: Pa55w.rd

> **Note**: Lab virtual machine sign in instructions will be provided to you by your instructor.

#### Review installed applications

Observe the taskbar located at the bottom of your **Windows 10** desktop. The taskbar contains the icons for the applications you will use in this lab:

-   Microsoft Edge

-   File Explorer

-   Visual Studio Code

#### Download the lab files

1.  On the taskbar, select the **Windows PowerShell** icon.

1.  In the PowerShell command prompt, change the current working directory to the **Allfiles (F):\\** path:

    ```powershell
    cd F:
    ```

1.  Within the command prompt, enter the following command and press Enter to clone the **microsoftlearning/AZ-203-DevelopingSolutionsforMicrosoftAzure** project hosted on GitHub into the **Allfiles (F):\\** drive:

    ```powershell
    git clone --depth 1 --no-checkout https://github.com/microsoftlearning/AZ-203-DevelopingSolutionsForMicrosoftAzure .
    ```

1.  Within the command prompt, enter the following command and press **Enter** to check out the lab files necessary to complete the **AZ-203T03** lab:

    ```powershell
    git checkout master -- Allfiles/*
    ```

1.  Close the currently running **Windows PowerShell** command prompt application.

### Exercise 1: Creating database resources in Azure

#### Task 1: Open the Azure portal

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, navigate to the **Azure portal** ([portal.azure.com](https://portal.azure.com)).

1.  Enter the **email address** for your Microsoft account.

1.  Select **Next**.

1.  Enter the **password** for your Microsoft account.

1.  Select **Sign in**.

    > **Note**: If this is your first time signing in to the **Azure Portal**, a dialog box will appear offering a tour of the portal. Select **Get Started** to skip the tour and begin using the portal.

#### Task 2: Create an Azure Cache for Redis resource

1.  In the navigation pane on the left side of the Azure portal, select **All services**.

1.  In the **All services** blade, select **Azure Cache for Redis**.

1.  In the **Azure Cache for Redis** blade, view the list of your Redis cache instances.

1.  At the top of the **Azure Cache for Redis** blade, select **+ Add**.

1.  In the **New Redis Cache** blade, perform the following actions:

    1.  IN the **DNS name** field, enter the value **polyrediscache\[your name in lowercase\]**

    1.  Leave the **Subscription** drop-down list set to its default value.

    1.  In the **Resource group** section, select **Create new**, enter **PolyglotData**, and then select **OK**.

    1.  In the **Location** drop-down list, select the **East US** option.

    1.  In the **Pricing tier** list, select the **Basic C0 (250MB Cache)** option.

    1.  In the **Unblock port 6379 (not SSL encrypted)** section, ensure the checkbox is not selected.

    1. Select **Create**.

1.  Wait for the creation task to complete before you move forward with this lab.

    > **Note**: An Azure Cache for Redis resource can take anywhere from **15-30 minutes** to become ready for use. You can choose to move forward with the lab, but you must remember that this resource and its connection string is required for **Exercise 6: Authoring .NET code to connect to Azure Redis Cache**.

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polyrediscache\*** Azure Cache for Redis instance that you created earlier in this lab.

1.  In the **Azure Cache for Redis** blade, locate the **Settings** section on the left side of the blade and select the **Access keys** link.

1.  In the **Access keys** pane, record the value in the **Primary connection string (StackExchange.Redis)** field. You will use this value later in this lab.

#### Task 3: Create an Azure SQL server resource

1.  In the navigation pane on the left side of the Azure portal, select **All services**.

1.  In the **All services** blade, select **SQL servers**.

1.  In the **SQL servers** blade, view your list of SQL server instances.

1.  At the top of the **SQL servers** blade, select **+ Add**.

1.  In the **Create SQL Database Server** blade, observe the tabs at the top of the blade, such as **Basics**, **Networking** and **Additional settings**.

    > **Note**: Each tab represents a step in the workflow to create a new **Azure SQL Database server**. At any time, you can select **Review + create** to skip the remaining tabs.

1.  In the **Basics** tab, perform the following actions:

    1.  Leave the **Subscription** drop-down list set to its default value.

    1.  In the **Resource group** section, select **PolyglotData** from the list.

    1.  In the **Server name** field, enter the value **polysqlsrvr\[your name in lowercase\]**.

    1.  In the **Location** drop-down list, select the **(US) East US** option.

    1.  In the **Server admin login** field, enter the value **testuser**.

    1.  In the **Password** field, enter the value **TestPa$$w0rd**.

    1.  In the **Confirm password** field, enter the value **TestPa$$w0rd** again.

    1.  Select **Next: Networking >**.

1.  In the **Networking** tab, perform the following actions:

    1. In the **Allow Azure services and resources to access this server** section, select **Yes**.

    1.  Select **Review + Create**.

1.  In the **Review + Create** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the Azure SQL Database server by using your specified configuration.

1.  Wait for the creation task to complete before you move forward with this lab.

#### Task 4: Create an Azure Cosmos DB account resource

1.  In the navigation pane on the left side of the Azure portal, select **All services**.

1.  In the **All services** blade, select **Azure Cosmos DB**.

1.  In the **Azure Cosmos DB** blade, view your list of Azure Cosmos DB instances.

1.  At the top of the **Azure Cosmos DB** blade, select **+ Add**.

1.  In the **Create Azure Cosmos DB Account** blade, observe the tabs at the top of the blade, such as **Basics**, **Network** and **Tags**.

    > **Note**: Each tab represents a step in the workflow to create a new **Azure Cosmos DB account**. At any time, you can select **Review + create** to skip the remaining tabs.

1.  In the **Basics** tab, perform the following actions:

    1.  Leave the **Subscription** list set to its default value.

    1.  In the **Resource group** section, select **PolyglotData** from the list.

    1.  In the **AccountName** field, enter **polycosmos\[your name in lowercase\]**.

    1.  In the **API** drop-down list, select the **Core (SQL)** option.

    1.  In the **Location** drop-down list, select the **East US** region.

    1.  In the **Geo-Redundancy** section, select the **Disable** option.

    1.  In the **Multi-region Writes** section, select the **Disable** option.

    1.  Select **Review + Create**.

1.  In the **Review + Create** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the Azure Cosmos DB account by using your specified configuration.

1.  Wait for the creation task to complete before you move forward with this lab.

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polycosmos\*** Azure Cosmos DB account that you created earlier in this lab.

1.  In the **Azure Cosmos DB account** blade, locate the **Settings** section on the left side of the blade and select the **Keys** link.

1.  In the **Keys** pane, record the value in the **PRIMARY CONNECTION STRING** field. You will use this value later in this lab.

#### Task 5: Create an Azure Storage account resource

1.  In the navigation pane on the left side of the Azure portal, select **All services**.

1.  In the **All services** blade, select **Storage Accounts**.

1.  In the **Storage accounts** blade, view your list of Storage instances.

1.  At the top of the **Storage accounts** blade, select **+ Add**.

1.  In the **Create storage account** blade, observe the tabs at the top of the blade, such as **Basics**, **Advanced** and **Tags**.

    > **Note**: Each tab represents a step in the workflow to create a new **Azure Storage Account**. At any time, you can select **Review + create** to skip the remaining tabs.

1.  In the **Basics** tab, perform the following actions:

    1.  Leave the **Subscription** list set to its default value.

    1.  In the **Resource group** section, select **PolyglotData** from the list.

    1.  In the **Storage account name** field, enter **polystor\[your name in lowercase\]**.

    1.  In the **Location** drop-down list, select the **East US** region.

    1.  In the **Performance** section, select **Standard**.

    1.  In the **Account kind** drop-down list, select **StorageV2 (general purpose v2)**.

    1.  In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.

    1.  In the **Access tier (default)** section, ensure that **Hot** is selected.

    1.  Select **Review + Create**.

1.  In the **Review + Create** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the storage account by using your specified configuration.

1.  Wait for the creation task to complete before you move forward with this lab.

#### Review

In this exercise, you created all the Azure resources that you will need for a polyglot data solution.

### Exercise 2: Import databases and images

#### Task 1: Upload image blobs

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polystor\*** storage account that you created earlier in this lab.

1.  In the **Storage account** blade, select the **Containers** link located in the **Blob service** section on the left side of the blade.

1.  In the **Containers** section, select **+ Container**.

1.  In the **New container** pop-up, perform the following actions:

    1.  In the **Name** field, enter **images**.

    1.  In the **Public access level** drop-down list, select **Blob (anonymous read access for blobs only)**.

    1.  Select **OK**.

1.  Back in the **Containers** section, select the newly created **images** container.

1.  In the **Container** blade, locate the **Settings** section on the left side of the blade and select the **Properties** link.

1.  In the **Properties** pane, record the value in the **URL** field. You will use this value later in this lab.

1.  Locate and select the **Overview** link on the left side of the blade.

1.  At the top of the blade, select **Upload**.

1.  In the **Upload blob** pop-up, perform the following actions:

    1.  In the **Files** section, select the **Folder** icon.

    1.  In the File Explorer dialog box, go to **Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\Images**, select all fourty-two **.jpg** image files, and then select **Open**.

    1.  Ensure that **Overwrite if files already exist** is selected.

    1.  Select **Upload**.

1. Wait for all of the blobs to be uploaded before you continue with this lab.

#### Task 2: Upload SQL .bacpac file

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polystor\*** storage account that you created earlier in this lab.

1.  In the **Storage account** blade, select the **Containers** link located in the **Blob service** section on the left side of the blade.

1.  In the **Containers** section, select **+ Container**.

1.  In the **New container** pop-up, perform the following actions:

    1.  In the **Name** field, enter **databases**.

    1.  In the **Public access level** drop-down list, select **Private (no anonymous access)**.

    1.  Select **OK**.

1.  Back in the **Containers** section, select the newly created **databases** container.

1.  In the **Container** blade, select **Upload**.

1.  In the **Upload blob** pop-up, perform the following actions:

    1.  In the **Files** section, select the **Folder** icon.

    1.  In the File Explorer dialog box, go to **Allfiles (F):\\Allfiles\\Labs\\03\\Starter**, select the **AdventureWorks.bacpac** file, and then select **Open**.

    1.  Ensure that **Overwrite if files already exist** is selected.

    1.  Select **Upload**.

1. Wait for the blob to be uploaded before you continue with this lab.

#### Task 3: Import SQL database

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polysqlsrvr\*** SQL server that you created earlier in this lab.

1.  In the **SQL server** blade, select **Import database**.

1.  In the **Import database** blade that appears, perform the following actions:

    1.  Leave the **Subscription** list set to its default value.

    1.  Select the **Storage** option.

    1.  In the **Storage accounts** blade that appears, select the **polystor\*** storage account that you created earlier in this lab.

    1.  In the **Containers** blade that appears, select the **databases** container that you created earlier in this lab.

    1.  In the **Container** blade that appears, select the **AdventureWorks.bacpac** blob that you created earlier in this lab and then select **Select** to close the blade.

    1.  Back in the **Import database** blade, leave the **Pricing tier** option set to its default value.

    1.  In the **Database name** field, enter **AdventureWorks**.

    1.  Leave the **Collation** field set to its default value.

    1.  In the **Server admin login** field, enter the value **testuser**.

    1.  In the **Password** field, enter the value **TestPa$$w0rd**.

    1.  Select **OK**.

1. Wait for the database to be created before you continue with this lab.

#### Task 4: Use imported SQL Database

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polysqlsrvr\*** SQL server that you created earlier in this lab.

1.  In the **SQL server** blade, locate the **Security** section on the left side of the blade and select the **Firewalls and virtual networks** link.

1.  In the **Firewalls and virtual networks** pane, select **Add client IP** and then select **Save**.

    > **Note**: This step will ensure that your local machine will have access to the databases associated with this server.

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **AdventureWorks** SQL database that you created earlier in this lab.

1.  In the **SQL database** blade, locate the **Settings** section on the left side of the blade and select the **Connection strings** link.

1.  In the **Connection strings** pane, record the value in the **ADO.NET (SQL Authentication)** field. You will use this value later in this lab.

1.  Update the connection string you recorded by performing the following actions:

    1.  Within the connection string, locate the ``{your_username}`` placeholder and replace it with ``testuser``.

    1.  Within the connection string, locate the ``{your_password}`` placeholder and replace it with ``TestPa$$w0rd``.

        > **Note**: For example, if your connection string was originally ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID={your_username};Password={your_password};``, your updated connection string will be ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID=testuser;Password=TestPa$$w0rd;``

1.  Locate and select the **Query editor** link on the left side of the blade.

1.  In the **Query editor** pane, perform the following actions:

    1.  In the **Login** field, enter the value **testuser**.

    1.  In the **Password** field, enter the value **TestPa$$w0rd**.

    1.  Select **OK**.

1.  In the open query editor, enter the following query:

    ```sql
    SELECT * FROM AdventureWorks.dbo.Models
    ```

1.  Select **Run** to execute the query.

1.  Observe the results of the query.

    > **Note**: This query will return a list of models that will appear on the homepage of the web application.

1.  In the query editor, replace the existing query with the following query:

    ```sql
    SELECT * FROM AdventureWorks.dbo.Products
    ```

1.  Select **Run** to execute the query.

1.  Observe the results of the query.

    > **Note**: This query will return a list of products associated with each model.

#### Review

In this exercise, you imported all of the resources you will use with your web application.

### Exercise 3: Open and configure a .NET Core web application

#### Task 1: Open and build the web application

1.  On the **Start** screen, select the **Visual Studio Code** tile.

1.  On the **File** menu, select **Open Folder**.

1.  In the File Explorer pane that opens, go to **Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\AdventureWorks**, and then select **Select Folder**.

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

    > **Note**: The ``dotnet build`` command will automatically restore any missing NuGet packages prior to building all projects in the folder.

1.  Observe the results of the build printed in the terminal. The build should complete successfully with no errors or warning messages.

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 2: Update SQL connection string

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Web** project.

1.  Double-click (or double-select) the **appsettings.json** file.

1.  In the JSON object, in line 3, locate the **ConnectionStrings.AdventureWorksSqlContext** path. Observe that the current value is empty:

    ```json
    "ConnectionStrings": {
        "AdventureWorksSqlContext": "",
        "AdventureWorksCosmosContext": "",
        "AdventureWorksRedisContext": ""
    },
    ```

1.  Update the value of the **AdventureWorksSqlContext** property by setting its value to the **ADO.NET (SQL Authentication) connection string** of the **SQL database** that you recorded earlier in this lab.

    > **Note**: It is important that you use your updated connection string here. The original connection string copied from the portal will not have the username and password necessary to connect to the SQL database.

1.  Save the **appsettings.json** file.

#### Task 3: Update blob base URL

1.  In the JSON object, in line 8, locate the **Settings.BlobContainerUrl** path. Observe that the current value is empty:

    ```json
    "Settings": {
        "BlobContainerUrl": "",
        "CartAvailable": false,
        "UniqueIdentifier": "az:dev:student"
    }
    ```

1.  Update the value of the **BlobContainerUrl** property by setting its value to the **URL** property of the **Azure Storage** blob container named **images** that you recorded earlier in this lab.

1.  Save the **appsettings.json** file.

#### Task 4: Validate web application

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Web** folder:

    ```powershell
    cd .\AdventureWorks.Web\
    ```

1.  In the command prompt, enter the following command and press Enter to run the .NET Core web application:

    ```powershell
    dotnet run
    ```

    > **Note**: The ``dotnet run`` command will automatically build any changes to the project and then start the web application without a debugger attached. The command will output the URL of the running application and any assigned ports.

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, navigate to the your currently running web application (<http://localhost:5000>).

1.  In the web application, observe the list of models displayed on the front page.

1.  Locate the **Water Bottle** model and select **View Details**.

1.  On the **Water Bottle** product detail page, select **Add to Cart**.

1.  Observe that the checkout functionality is currently disabled.

    > **Note**: For now, only the product page functionality is implemented. You will implement the checkout logic later in this lab.

1.  Close the browser window showing your web application.

1.  Return to the **Visual Studio Code** window.

1.  Back in the **Visual Studio Code** window, select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Review

In this exercise, you configured your ASP.NET Core web application to connect to your resources in Azure.

### Exercise 4: Migrating SQL data to Azure Cosmos DB

#### Task 1: Create migration project

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to create a new .NET project named **AdventureWorks.Migrate** in a folder with the same name:

    ```powershell
    dotnet new console --name AdventureWorks.Migrate --langVersion 7.1
    ```

    > **Note**: The ``dotnet new`` command will create a new **console** project in a folder with the same name as the project.

1.  In the command prompt, enter the following command and press Enter to add a reference to the existing **AdventureWorks.Models** project:

    ```powershell
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Models\AdventureWorks.Models.csproj
    ```

    > **Note**: The ``dotnet add reference`` command will add a reference to the model classes contained in the **AdventureWorks.Models** project.

1.  In the command prompt, enter the following command and press Enter to add a reference to the existing **AdventureWorks.Context** project:

    ```powershell
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Context\AdventureWorks.Context.csproj
    ```

    > **Note**: The ``dotnet add reference`` command will add a reference to the context classes contained in the **AdventureWorks.Context** project.

1.  In the command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Migrate** folder:

    ```powershell
    cd .\AdventureWorks.Migrate
    ```

1.  In the command prompt, enter the following command and press Enter to import version **2.2.6** of the **Microsoft.EntityFrameworkCore.SqlServer** from NuGet:

    ```powershell
    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 2.2.6
    ```

    > **Note**: The ``dotnet add package`` command will add the **[Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/2.2.6)** package from **NuGet**.

1.  In the command prompt, enter the following command and press Enter to import version **3.0.0** of the **Microsoft.Azure.Cosmos** from NuGet:

    ```powershell
    dotnet add package Microsoft.Azure.Cosmos --version 3.0.0
    ```

    > **Note**: The ``dotnet add package`` command will add the **[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.0.0)** package from **NuGet**.

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 2: Create .NET class

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Migrate** project.

1.  Double-click (or double-select) the **Program.cs** file.

1.  In the code editor tab for the **Program.cs** file, delete all code in the existing file.

1.  Add the following lines of code to import the **AdventureWorks.Models** and **AdventureWorks.Context** namespaces from the referenced **AdventureWorks.Models** and **AdventureWorks.Context** projects:

    ```cs
    using AdventureWorks.Context;
    using AdventureWorks.Models;
    ```

1.  Add the following line of code to import the **Microsoft.Azure.Cosmos** namespace from the **Microsoft.Azure.Cosmos** package imported from NuGet:

    ```cs
    using Microsoft.Azure.Cosmos;
    ```

1.  Add the following line of code to import the **Microsoft.EntityFrameworkCore** namespace from the **Microsoft.EntityFrameworkCore.SqlServer** package imported from NuGet:

    ```cs
    using Microsoft.EntityFrameworkCore;
    ```

1.  Add the following lines of code to add **using** directives for built-in namespaces that will be used in this file:

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  Enter the following code to create a new **Program** class:

    ```cs
    public class Program
    {
    }
    ```

1.  Within the **Program** class, enter the following line of code to create a new string constant named **sqlDBConnectionString**:

    ```cs
    private const string sqlDBConnectionString = "";
    ```

1.  Update the the **sqlDBConnectionString** string constant by setting its value to the **ADO.NET (SQL Authentication) connection string** of the **SQL database** that you recorded earlier in this lab.

    > **Note**: It is important that you use your updated connection string here. The original connection string copied from the portal will not have the username and password necessary to connect to the SQL database.

1.  Within the **Program** class, enter the following line of code to create a new string constant named **cosmosDBConnectionString**:

    ```cs
    private const string cosmosDBConnectionString = "";
    ```

1.  Update the the **cosmosDBConnectionString** string constant by setting its value to the **PRIMARY CONNECTION STRING** of the **Azure Cosmos DB account** that you recorded earier in this lab.

1.  Within the **Program** class, enter the following code to create a new asynchronous **Main** method:

    ```cs
    public static async Task Main(string[] args)
    {
    }
    ```

1.  Within the **Main** method, add the following line of code to print an introductory message to the console:

    ```cs
    await Console.Out.WriteLineAsync("Start Migration");
    ```

1.  Save the **Program.cs** file.

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Migrate** folder:

    ```powershell
    cd .\AdventureWorks.Migrate
    ```

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 3: Get SQL database records using Entity Framework

1.  Within the **Main** method of the **Program** class within the **Program.cs** file, add the following line of code to create a new instance of the **AdventureWorksSqlContext** class passing in the **sqlDBConnectionString** variable as the connection string value:

    ```cs
    AdventureWorksSqlContext context = new AdventureWorksSqlContext(sqlDBConnectionString);
    ```

1.  Within the **Main** method, add the following block of code to issue a LINQ query to get all **Models** and child **Products** from the database and store them in an in-memory **List<>** collection:

    ```cs
    List<Model> items = await context.Models
        .Include(m => m.Products)
        .ToListAsync<Model>();
    ```

1.  Within the **Main** method, add the following line of code to print out the number of records imported from **Azure SQL Database**:

    ```cs
    await Console.Out.WriteLineAsync($"Total Azure SQL DB Records: {items.Count}");
    ```

1.  Save the **Program.cs** file.

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Migrate** folder:

    ```powershell
    cd .\AdventureWorks.Migrate
    ```

1.  In the command prompt,  enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

    > **Note**: If there are any build errors, please review the **Program.cs** file located in the **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Migrate** folder.

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 4: Insert items into Azure Cosmos DB

1.  Within the **Main** method of the **Program** class within the **Program.cs** file, add the following line of code to create a new instance of the **CosmosClient** class passing in the **cosmosDBConnectionString** variable as the connection string value:

    ```cs
    CosmosClient client = new CosmosClient(cosmosDBConnectionString);
    ```

1.  Within the **Main** method, add the following line of code to create a new **database** named **Retail** if it does not already exist in the Azure Cosmos DB account:

    ```cs
    Database database = await client.CreateDatabaseIfNotExistsAsync("Retail");
    ```

1.  Within the **Main** method, add the following block of code to create a new **container** named **Online** if it does not already existing in the Azure Cosmos DB account with a partition key path of **/Category** and a throughput of **1000 RUs**:

    ```cs
    Container container = await database.CreateContainerIfNotExistsAsync("Online",
        partitionKeyPath: $"/{nameof(Model.Category)}",
        throughput: 1000
    );
    ```

1.  Within the **Main** method, add the following line of code to create an **int** variable named **count**:

    ```cs
    int count = 0;
    ```

1.  Within the **Main** method, add the following block of code to create a **foreach** loop that iterates over the objects in the **items** collection:

    ```cs
    foreach (var item in items)
    {
    }
    ```

1.  Within the **foreach** loop contained in **Main** method, add the following line of code to **upsert** the object into the Azure Cosmos DB collection and save the result in a variable of type **ItemResponse<>** named **document**:

    ```cs
    ItemResponse<Model> document = await container.UpsertItemAsync<Model>(item);
    ```

1.  Within the **foreach** loop contained in **Main** method, add the following line of code to print out the **activity id** of each upsert operation:

    ```cs
    await Console.Out.WriteLineAsync($"Upserted document #{++count:000} [Activity Id: {document.ActivityId}]");
    ```

1.  Back within the **Main** method (outside of the foreach loop), add the following line of code to print out the number of documents exported to **Azure Cosmos DB**:

    ```cs
    await Console.Out.WriteLineAsync($"Total Azure Cosmos DB Documents: {count}");
    ```

1.  Save the **Program.cs** file.

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Migrate** folder:

    ```powershell
    cd .\AdventureWorks.Migrate
    ```

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

    > **Note**: If there are any build errors, please review the **Program.cs** file located in the **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Migrate** folder.

#### Task 5: Perform migration

1.  In the open command prompt, enter the following command and press Enter to run the .NET Core web application:

    ```powershell
    dotnet run
    ```

    > **Note**: The ``dotnet run`` command will start the console application.

1.  Observe the various data that is printed to the screen including; initial SQL record count, individual upsert activity identifiers, final Azure Cosmos DB document count.

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 6: Validate migration

1.  Return to the **Microsoft Edge** browser window showing the **Azure portal**.

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **PolyglotData** resource group that you created earlier in this lab.

1.  In the **PolyglotData** blade, select the **polycosmos\*** Azure Cosmos DB account that you created earlier in this lab.

1.  In the **Azure Cosmos DB account** blade, locate and select the **Data Explorer** link on the left side of the blade.

1.  In the **Data Explorer** pane, expand the **Retail** database node.

1.  Expand the **Online** container node.

1.  Select **New SQL Query**.

    > **Note**: The label for this option may be hidden. You can view labels by hovering over the icons at the top of the **Data Explorer** pane.

1.  In the query tab that appears, enter the following text:

    ```sql
    SELECT * FROM models
    ```

1.  Select **Execute Query**.

1.  Observe the list of JSON models returned by the query.

1.  Back in the query editor, replace the existing text with the following text:

    ```sql
    SELECT VALUE COUNT(1) FROM models
    ```

1.  Select **Execute Query**.

1.  Observe the result of the **COUNT** aggregate operation.

1.  Return to the **Visual Studio Code** window.

#### Review

In this exercise, you used Entity Framework and the .NET SDK for Azure Cosmos DB to migrate data from Azure SQL Database to Azure Cosmos DB.

### Exercise 5: Accessing Azure Cosmos DB using .NET

#### Task 1: Update Library with the Cosmos SDK and references

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Context** folder:

    ```powershell
    cd .\AdventureWorks.Context\
    ```

1.  In the command prompt, enter the following command and press Enter to import the **Microsoft.Azure.Cosmos** from NuGet:

    ```powershell
    dotnet add package Microsoft.Azure.Cosmos --version 3.0.0
    ```

    > **Note**: The ``dotnet add package`` command will add the **[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.0.0)** package from **NuGet**.

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 2: Write .NET code to connect to Azure Cosmos DB

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Context** project.

1.  Access the context menu or right-click the **AdventureWorks.Context** folder node and then select **New File**.

1.  In the prompt that appears, enter the value **AdventureWorksCosmosContext.cs**.

1.  In the code editor tab for the **AdventureWorksCosmosContext.cs** file, add the following lines of code to import the **AdventureWorks.Models** namespace from the referenced **AdventureWorks.Models** project:

    ```cs
    using AdventureWorks.Models;
    ```

1.  Add the following lines of code to import the **Microsoft.Azure.Cosmos** and **Microsoft.Azure.Cosmos.Linq** namespaces from the **Microsoft.Azure.Cosmos** package imported from NuGet:

    ```cs
    using Microsoft.Azure.Cosmos;
    using Microsoft.Azure.Cosmos.Linq;
    ```

1.  Add the following lines of code to add **using** directives for built-in namespaces that will be used in this file:

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  Enter the following code to add a **AdventureWorks.Context** namespace block:

    ```cs
    namespace AdventureWorks.Context
    {
    }
    ```

1.  Within the **AdventureWorks.Context** namespace, enter the following code to create a new **AdventureWorksCosmosContext** class:

    ```cs
    public class AdventureWorksCosmosContext
    {
    }
    ```

1.  Update the declaration of the **AdventureWorksCosmosContext** class by adding a specification indicating that this class will implement the **IAdventureWorksProductContext** interface:

    ```cs
    public class AdventureWorksCosmosContext : IAdventureWorksProductContext
    {
    }
    ```

1.  Within the **AdventureWorksCosmosContext** class, enter the following line of code to create a new readonly **Container** variable named **_container**:

    ```cs
    private readonly Container _container;
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new constructor with the following signature:

    ```cs
    public AdventureWorksCosmosContext(string connectionString, string database = "Retail", string container = "Online")
    {
    }
    ```

1.  Within the constructor, add the following block of code to create a new instance of the **CosmosClient** class and then obtain both a **Database** and **Container** instance from the client:

    ```cs
    _container = new CosmosClient(connectionString)
        .GetDatabase(database)
        .GetContainer(container);
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new **FindModelAsync** method with the following signature:

    ```cs
    public async Task<Model> FindModelAsync(Guid id)
    {
    }
    ```

1.  Within the **FindModelAsync** method, add the following blocks of code to create a LINQ query, transform it into an iterator, iterate over the result set, and then return the single item in the result set:

    ```cs
    var iterator = _container.GetItemLinqQueryable<Model>()
        .Where(m => m.id == id)
        .ToFeedIterator<Model>();

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new **GetModelsAsync** method with the following signature:

    ```cs
    public async Task<List<Model>> GetModelsAsync()
    {
    }
    ```

1.  Within the **GetModelsAsync** method, add the following blocks of code to execute a sql query, get the query result iterator, iterator over the result set, and then return the union of all results:

    ```cs
    string query = $@"SELECT * FROM items";

    var iterator = _container.GetItemQueryIterator<Model>(query);

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches;
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new **FindProductAsync** method with the following signature:

    ```cs
    public async Task<Product> FindProductAsync(Guid id)
    {
    }
    ```

1.  Within the **FindProductAsync** method, add the following blocks of code to execute a sql query, get the query result iterator, iterates over the result set, and then return the single item in the result set:

    ```cs
    string query = $@"SELECT VALUE products
                        FROM models
                        JOIN products in models.Products
                        WHERE products.id = '{id}'";

    var iterator = _container.GetItemQueryIterator<Product>(query);

    List<Product> matches = new List<Product>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  Save the **AdventureWorksCosmosContext.cs** file.

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Context** folder:

    ```powershell
    cd .\AdventureWorks.Context
    ```

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

    > **Note**: If there are any build errors, please review the **AdventureWorksCosmosContext.cs** file located in the **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Context** folder.

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 3: Update Azure Cosmos DB connection string

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Web** project.

1.  Double-click (or double-select) the **appsettings.json** file.

1.  In the JSON object, in line 4, locate the **ConnectionStrings.AdventureWorksCosmosContext** path. Observe that the current value is empty:

    ```json
    "ConnectionStrings": {
        "AdventureWorksSqlContext": "<sql-connection-string>",
        "AdventureWorksCosmosContext": "",
        "AdventureWorksRedisContext": ""
    },
    ```

1.  Update the value of the **AdventureWorksCosmosContext** property by setting its value to the **PRIMARY CONNECTION STRING** of the **Azure Cosmos DB account** that you recorded earier in this lab.

1.  Save the **appsettings.json** file.

#### Task 4: Update .NET application startup logic

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Web** project.

1.  Double-click (or double-select) the **Startup.cs** file.

1.  In the **Startup** class, locate the existing **ConfigureProductService** method:

    ```cs
    public void ConfigureProductService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksProductContext, AdventureWorksSqlContext>(provider =>
            new AdventureWorksSqlContext(
                _configuration.GetConnectionString(nameof(AdventureWorksSqlContext))
            )
        );
    }
    ```

    > **Note**: The current product service uses SQL as its database.

1.  Within the **ConfigureProductService** method, delete all existing lines of code :

    ```cs
    public void ConfigureProductService(IServiceCollection services)
    {
    }
    ```

1.  Within the **ConfigureProductService** method, add the following block of code to change the products provider to the **AdventureWorksCosmosContext** implementation you created earlier in this lab:

    ```cs
    services.AddScoped<IAdventureWorksProductContext, AdventureWorksCosmosContext>(provider =>
        new AdventureWorksCosmosContext(
            _configuration.GetConnectionString(nameof(AdventureWorksCosmosContext))
        )
    );
    ```

1.  Save the **Startup.cs** file.

#### Task 5: Validate .NET application successfully connects to Azure Cosmos DB

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Web** folder:

    ```powershell
    cd .\AdventureWorks.Web\
    ```

1.  In the command prompt, enter the following command and press Enter to run the .NET Core web application:

    ```powershell
    dotnet run
    ```

    > **Note**: The ``dotnet run`` command will automatically build any changes to the project and then start the web application without a debugger attached. The command will output the URL of the running application and any assigned ports.

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, navigate to the your currently running web application (<http://localhost:5000>).

1.  In the web application, observe the list of models displayed on the front page.

1.  Locate the **Touring-1000** model and select **View Details**.

1.  On the **Touring-1000** product detail page, perform the following actions:

    1.  In the **Select options** list, select **Touring-1000 Yellow, 50, $2,384.07**.

    1.  Select **Add to Cart**.

1.  Observe that the checkout functionality is still disabled.

    > **Note**: In the next exercise, you will implement the checkout logic.

1.  Close the browser window showing your web application.

1.  Return to the **Visual Studio Code** window.

1.  Back in the **Visual Studio Code** window, select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Review

In this exercise, you wrote C# code to query an Azure Cosmos DB collection using the .NET SDK.

### Exercise 6: Accessing Azure Cache for Redis using .NET

#### Task 1: Update Library with the StackExchange.Redis SDK and references

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Context** folder:

    ```powershell
    cd .\AdventureWorks.Context\
    ```

1.  In the command prompt, enter the following command and press Enter to import the **Newtonsoft.Json** from NuGet:

    ```powershell
    dotnet add package Newtonsoft.Json --version 12.0.2
    ```

    > **Note**: The ``dotnet add package`` command will add the **[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/12.0.2)** package from **NuGet**.

1.  In the command prompt, enter the following command and press Enter to import the **StackExchange.Redis** from NuGet:

    ```powershell
    dotnet add package StackExchange.Redis --version 2.0.601
    ```

    > **Note**: The ``dotnet add package`` command will add the **[StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/2.0.601)** package from **NuGet**.

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 2: Write .NET code to connect to Azure Cache for Redis

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Context** project.

1.  Access the context menu or right-click the **AdventureWorks.Context** folder node and then select **New File**.

1.  In the prompt that appears, enter the value **AdventureWorksRedisContext.cs**.

1.  In the code editor tab for the **AdventureWorksRedisContext.cs** file, add the following lines of code to import the **AdventureWorks.Models** namespace from the referenced **AdventureWorks.Models** project:

    ```cs
    using AdventureWorks.Models;
    ```

1.  Add the following lines of code to import the **Newtonsoft.Json** namespace from the **Newtonsoft.Json** package imported from NuGet:

    ```cs
    using Newtonsoft.Json;
    ```

1.  Add the following lines of code to import the **StackExchange.Redis** namespace from the **StackExchange.Redis** package imported from NuGet:

    ```cs
    using StackExchange.Redis;
    ```

1.  Add the following lines of code to add **using** directives for built-in namespaces that will be used in this file:

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  Enter the following code to add a **AdventureWorks.Context** namespace block:

    ```cs
    namespace AdventureWorks.Context
    {
    }
    ```

1.  Within the **AdventureWorks.Context** namespace, enter the following code to create a new **AdventureWorksRedisContext** class:

    ```cs
    public class AdventureWorksRedisContext
    {
    }
    ```

1.  Update the declaration of the **AdventureWorksRedisContext** class by adding a specification indicating that this class will implement the **IAdventureWorksCheckoutContext** interface:

    ```cs
    public class AdventureWorksRedisContext : IAdventureWorksCheckoutContext
    {
    }
    ```

1.  Within the **AdventureWorksRedisContext** class, enter the following line of code to create a new readonly **IDatabase** variable named **_database**:

    ```cs
    private readonly IDatabase _database;
    ```

1.  Within the **AdventureWorksRedisContext** class, add a new constructor with the following signature:

    ```cs
    public AdventureWorksRedisContext(string connectionString)
    {
    }
    ```

1.  Within the constructor, add the following block of code to create a new instance of the **ConnectionMultiplexer** class and then get the database instance:

    ```cs
    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect(connectionString);
    _database = connection.GetDatabase();
    ```

1.  Within the **AdventureWorksRedisContext** class, add a new **AddProductToCartAsync** method with the following signature:

    ```cs
    public async Task AddProductToCartAsync(string uniqueIdentifier, Product product)
    {
    }
    ```

1.  Within the **AddProductToCartAsync** method, add the following blocks of code to get the current value from a key, create a new list if one does not already exists, add the product to the list, and then store the list as the new value for the key in the database:

    ```cs
    RedisValue result = await _database.StringGetAsync(uniqueIdentifier);
    List<Product> products = new List<Product>();
    if (!result.IsNullOrEmpty)
    {
        List<Product> parsed = JsonConvert.DeserializeObject<List<Product>>(result.ToString());
        products.AddRange(parsed);
    }
    products.Add(product);
    string json = JsonConvert.SerializeObject(products);
    await _database.StringSetAsync(uniqueIdentifier, json);
    ```

1.  Within the **AdventureWorksRedisContext** class, add a new **GetProductsInCartAsync** method with the following signature:

    ```cs
    public async Task<List<Product>> GetProductsInCartAsync(string uniqueIdentifier)
    {
    }
    ```

1.  Within the **GetProductsInCartAsync** method, add the following lines of code to get the list from the database and parse the JSON value into a collection of **Product** instances:

    ```cs
    string json = await _database.StringGetAsync(uniqueIdentifier);
    List<Product> products = JsonConvert.DeserializeObject<List<Product>>(json ?? "[]");
    return products;
    ```

1.  Within the **AdventureWorksRedisContext** class, add a new **ClearCart** method with the following signature:

    ```cs
    public async Task ClearCart(string uniqueIdentifier)
    {
    }
    ```

1.  Within the **ClearCart** method, add the following line of code to remove a key and its associated values from the database:

    ```cs
    await _database.KeyDeleteAsync(uniqueIdentifier);
    ```

1.  Save the **AdventureWorksRedisContext.cs** file.

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Context** folder:

    ```powershell
    cd .\AdventureWorks.Context
    ```

1.  In the command prompt, enter the following command and press Enter to build the .NET Core web application:

    ```powershell
    dotnet build
    ```

    > **Note**: If there are any build errors, please review the **AdventureWorksRedisContext.cs** file located in the **Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\AdventureWorks\\AdventureWorks.Context** folder.

1.  Select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Task 3: Update Redis connection string

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Web** project.

1.  Double-click (or double-select) the **appsettings.json** file.

1.  In the JSON object, in line 4, locate the **ConnectionStrings.AdventureWorksRedisContext** path. Observe that the current value is empty:

    ```powershell
    "ConnectionStrings": {
        "AdventureWorksSqlContext": "<sql-connection-string>",
        "AdventureWorksCosmosContext": "<cosmos-connection-string>",
        "AdventureWorksRedisContext": ""
    },
    ```

1.  Update the value of the **AdventureWorksRedisContext** property by setting its value to the **Primary connection string (StackExchange.Redis)** of the **Azure Cache for Redis** instance that you recorded earier in this lab.

1.  In the JSON object, in line 9, locate the **Settings.CartAvailable** path. Observe that the current value is **false**:

    ```powershell
    "Settings": {
        "BlobContainerUrl": "<blob-container-base-uri>",
        "CartAvailable": false,
        "UniqueIdentifier": "az:dev:student"
    }
    ```

1.  Update the value of the **CartAvailable** property by setting its value to **true**:

    ```powershell
    "CartAvailable": true,
    ```

1.  Save the **appsettings.json** file.

#### Task 4: Update .NET application startup logic

1.  In the **Explorer** pane of the Visual Studio Code window, expand the **AdventureWorks.Web** project.

1.  Double-click (or double-select) the **Startup.cs** file.

1.  In the **Startup** class, locate the existing **ConfigureCheckoutService** method:

    ```powershell
    public void ConfigureCheckoutService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksCheckoutContext>(provider =>
            new Mock<IAdventureWorksCheckoutContext>().Object
        );
    }
    ```

    > **Note**: The current checkout service uses a mock as its database.

1.  Within the **ConfigureCheckoutService** method, delete all existing lines of code :

    ```powershell
    public void ConfigureCheckoutService(IServiceCollection services)
    {
    }
    ```

1.  Within the **ConfigureCheckoutService** method, add the following block of code to change the checkout provider to the **AdventureWorksRedisContext** implementation you created earlier in this lab:

    ```powershell
    services.AddScoped<IAdventureWorksCheckoutContext, AdventureWorksRedisContext>(provider =>
        new AdventureWorksRedisContext(
            _configuration.GetConnectionString(nameof(AdventureWorksRedisContext))
        )
    );
    ```

1.  Save the **Startup.cs** file.

#### Task 5: Validate .NET application successfully connects to Azure Cache for Redis

1.  In the Visual Studio Code window, access the context menu or right-click the **Explorer** pane and then select **Open in Terminal**.

1.  In the open command prompt, enter the following command and press Enter to switch your terminal context to the **AdventureWorks.Web** folder:

    ```powershell
    cd .\AdventureWorks.Web\
    ```

1.  In the command prompt, enter the following command and press Enter to run the .NET Core web application:

    ```powershell
    dotnet run
    ```

    > **Note**: The ``dotnet run`` command will automatically build any changes to the project and then start the web application without a debugger attached. The command will output the URL of the running application and any assigned ports.

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, navigate to the your currently running web application (<http://localhost:5000>).

1.  In the web application, observe the list of models displayed on the front page.

1.  Locate the **Mountain-400-W** model and select **View Details**.

1.  On the **Mountain-400-W** product detail page, perform the following actions:

    1.  In the **Select options** list, select **Mountain-400-W Silver, 40, $769.49**.

    1.  Select **Add to Cart**.

1.  On the shopping cart page, observe the contents of the cart and then select **Checkout**.

1.  On the checkout page, observe the final receipt.

1.  Select the **Shopping Cart** icon at the top of the page.

1.  On the shopping cart page, observe the empty cart.

1.  Close the browser window showing your web application.

1.  Back in the **Visual Studio Code** window, select the **Trash Can** icon to dispose of the currently open terminal and any associated processes.

#### Review

In this exercise, you used C# code to store and retrieve data from an Azure Cache for Redis store.

### Exercise 7: Clean up subscription

#### Task 1: Open Azure Cloud Shell

1.  At the top of the portal, select the **Cloud Shell** icon to open a new shell instance.

    > **Note**: The **Cloud Shell** icon is represented by a greater than symbol and underscore character.

1.  If this is your first time opening the **Cloud Shell** by using your subscription, a **Welcome to Azure Cloud Shell Wizard** will appear that allows you to configure **Cloud Shell** for first-time usage. Perform the following actions in the wizard:

    1.  A dialog box will appear that prompts you to create a new Storage Account to begin using the shell. Accept the default settings and select **Create storage**.

    1.  Wait for the **Cloud Shell** to finish its first-time setup procedures before moving forward with the lab.

    > **Note**: If you do not see the configuration options for the **Cloud Shell**, this is most likely because you are using an existing subscription with this course's labs. The labs are written from the presumption that you are using a new subscription.

1.  In the **Cloud Shell** command prompt at the bottom of the portal, type in the following command and press Enter to list all resource groups in the subscription:

    ```powershell
    az group list
    ```
1.  In the prompt, type the following command and press Enter to view a list of possible commands to delete a resource group:

    ```powershell
    az group delete --help
    ```

#### Task 2: Delete resource groups

1.  In the prompt, type the following command and press Enter to delete the **PolyglotData** resource group:

    ```powershell
    az group delete --name PolyglotData --no-wait --yes
    ```

1.  Close the **Cloud Shell** pane at the bottom of the portal.

#### Task 3: Close active applications

1.  Close the currently running **Microsoft Edge** application.

1.  Close the currently running **Visual Studio Code** application.

#### Review

In this exercise, you cleaned up your subscription by removing the **resource groups** used in this lab.
