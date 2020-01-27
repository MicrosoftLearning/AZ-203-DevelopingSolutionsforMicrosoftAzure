---
lab:
    title: 'Lab: Access resource secrets securely across services'
    type: 'Answer Key'
    module: 'AZ-203T04-A: Implement Azure security'
---

# Lab: Access resource secrets securely across services
# Student lab answer key

## Microsoft Azure user interface

Given the dynamic nature of Microsoft cloud tools, you might experience Azure user interface (UI) changes after the development of this training content. These changes might cause the lab instructions and lab steps to not match up.

Microsoft updates this training course as soon as the community brings needed changes to our attention. However, because cloud updates occur frequently, you might encounter UI changes before this training content is updated. **If this occurs, adapt to the changes and work through them in the labs as needed.**

## Instructions

### Before you start

#### Sign in to the lab virtual machine

Sign in to your **Windows 10** virtual machine by using the following credentials:

-   **Username**: Admin

-   **Password**: Pa55w.rd

> **Note**: Lab virtual machine sign-in instructions will be provided to you by your instructor.

#### Review installed applications

Observe the taskbar located at the bottom of your **Windows 10** desktop. The taskbar contains the icons for the applications you will use in this lab:

-   Microsoft Edge

-   File Explorer

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

1.  Within the command prompt, enter the following command and press **Enter** to check out the lab files necessary to complete the **AZ-203T04** lab:

    ```powershell
    git checkout master -- Allfiles/*
    ```

1.  Close the currently running **Windows PowerShell** command prompt application.

### Exercise 1: Create Azure resources

#### Task 1: Open the Azure portal

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, navigate to the **Azure portal** ([portal.azure.com](https://portal.azure.com)).

1.  Enter the **email address** for your Microsoft account.

1.  Select **Next**.

1.  Enter the **password** for your Microsoft account.

1.  Select **Sign in**.

    > **Note**: If this is your first time signing in to the **Azure Portal**, a dialog box will appear offering a tour of the portal. Select **Get Started** to skip the tour and begin using the portal.

#### Task 2: Create an Azure Storage account

1.  In the navigation pane on the left side of the Azure portal, select **All services**.

1.  In the **All services** blade, select **Storage Accounts**.

1.  In the **Storage accounts** blade, view your list of Storage instances.

1.  At the top of the **Storage accounts** blade, select **+ Add**.

1.  In the **Create storage account** blade, observe the tabs at the top of the blade, such as **Basics**.

  > **Note**: Each tab represents a step in the workflow to create a new **storage account**. At any time, you can select **Review + create** to skip the remaining tabs.

1.  In the **Basics** tab, perform the following actions:

    1.  Leave the **Subscription** text box set to its default value.

    1.  In the **Resource group** section, select **Create new**, enter **SecureFunction**, and then select **OK**.

    1.  In the **Storage account** **name** text box, enter **securestor\[your name in lowercase\]**.

    1.  In the **Location** drop-down list, select the **(US) East US** region.

    1.  In the **Performance** section, select **Standard**.

    1.  In the **Account kind** drop-down list, select **StorageV2 (general purpose v2)**.

    1.  In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.

    1.  In the **Access tier** section, ensure that **Hot** is selected.

    1.  Select **Review + Create**.

1.  In the **Review + Create** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the storage account by using your specified configuration.

1.  Wait for the creation task to complete before you move forward with this lab.

1. In the navigation pane on the left side of the Azure portal, select **All services**.

1. In the **All services** blade, select **Storage Accounts**.

1. In the **Storage accounts** blade, select the storage account instance with the prefix **securestor**.

1. In the **Storage account** blade, locate the **Settings** section on the left side of the blade and select the **Access keys** link.

1. In the **Access keys** blade, select any one of the keys and record the value in either of the **Connection string** fields. You will use this value later in this lab.

    > **Note**: It does not matter which connection string you choose to use. They are interchangeable.

#### Task 3: Create an Azure Key Vault

1.  On the navigation menu located on the left side of the portal, select the **+ Create a resource** link.

1.  At the top of the **New** blade, locate the **Search the Marketplace** text box above the list of featured services.

1.  In the search text box, enter **Vault** and then press Enter.

1.  In the **Everything** search results blade, select the **Key Vault** result.

1.  In the **Key Vault** blade, select **Create**.

1.  In the **Create key vault** blade, observe the tabs at the top of the blade, such as **Basics**.

  > **Note**: Each tab represents a step in the workflow to create a new **key vault**. At any time, you can select **Review + create** to skip the remaining tabs.

1.  In the **Basics** tab, perform the following actions:

    1.  Leave the **Subscription** text box set to its default value.

    1.  In the **Resource group** section, **Use existing**, and then select **SecureFunction** from the list.

    1.  In the **Key vault name** text box, enter **securevault\[your name in lowercase\]**.

    1.  In the **Region** drop-down list, select the **East US** region.

    1.  In the **Pricing tier** drop-down list, select **Standard**.

    1.  Select **Review + Create**.

1.  In the **Review + Create** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the key vault by using your specified configuration.

1.  Wait for the creation task to complete before you move forward with this lab.

#### Task 4: Create an Azure Function app

1.  On the navigation menu located on the left side of the portal, select the **+ Create a resource** link.

1.  At the top of the **New** blade, locate the **Search the Marketplace** text box above the list of featured services.

1.  In the search text box, enter **Function** and then press Enter.

1.  In the **Everything** search results blade, select the **Function App** result.

1.  In the **Function App** blade, select **Create**.

1.  In the **Function App** blade, observe the tabs at the top of the blade, such as **Basics**.

  > **Note**: Each tab represents a step in the workflow to create a new **function app**. At any time, you can select **Review + create** to skip the remaining tabs.

1.  In the **Basics** tab, perform the following actions:

    1.  Leave the **Subscription** text box set to its default value.

    1.  In the **Resource group** section, **Use existing**, and then select **SecureFunction** from the list.

    1.  In the **Function app name** text box, enter **securefunc\[your name in lowercase\]**.

    1.  In the **Publish** section, select **Code**.

    1.  In the **Runtime stack** drop-down list, select **.NET Core**.

    1.  In the **Region** drop-down list, select the **East US** region.

    1.  Select **Next: Hosting**.

1.  In the **Hosting** tab, perform the following actions:

    1.  In the **Storage account** drop-down list, select the **securestor\*** Storage account that you created earlier in this lab.

    1.  In the **Operating System** section, select **Windows**.

    1.  In the **Plan type** drop-down list, select the **Consumption** option.

    1.  Select **Next: Monitoring**.

1.  In the **Monitoring** tab, perform the following actions:

    1.  In the **Enable Application Insights** section, select **No**.

    1.  Select **Review + Create**.

1.  In the **Review + Create** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the function app by using your specified configuration.

1.  Wait for the creation task to complete before you move forward with this lab.

#### Review

In this exercise, you created all the resources that you will use for this lab.

### Exercise 2: Configure secrets and identities

#### Task 1: Configure a system-assigned managed service identity

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securefunc\*** function app that you created earlier in this lab.

1.  In the **Function Apps** blade, select the **Platform features** tab.

1.  In the **Platform features** tab, select the **Identity** link located in the **Networking** section.

1.  In the **Identity** blade, locate the **System assigned** tab and then perform the following actions:

    1.  In the **Status** section, select **On**.

    1.  Select **Save**.

    1.  Select **Yes** in the confirmation dialog.

1.  Wait for the system-assigned managed identity to be created before you move forward with this lab.

#### Task 2: Create a Key Vault secret

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securevault\*** Key Vault that you created earlier in this lab.

1.  In the **Key Vault** blade, select the **Secrets** link located in the **Settings** section.

1.  In the **Secrets** pane, select **+ Generate/Import**.

1.  In the **Create a secret** blade, perform the following actions:

    1.  In the **Upload options** drop-down list, select **Manual**.

    1.  In the **Name** text box, enter **storagecredentials**.

    1.  In the **Value** text box, enter the storage account **Connection String** that you recorded earlier in this lab.

    1.  Leave the **Content Type** text box set to its default value.

    1.  Leave the **Set activation date** text box set to its default value.

    1.  Leave the **Set expiration date** text box set to its default value.

    1.  In the **Enabled** section, select **Yes**.

    1.  Select **Create**.

1.  Wait for the secret to be created before you move forward with this lab.

1.  Back in the **Secrets** pane, select the **storagecredentials** item in the list.

1.  In the **Versions** pane, select the latest version of the **storagecredentials** secret.

1. In the **Secret Version** pane, perform the following actions.

    1.  Observe the metadata for the latest version of the secret.

    1. Select **Show secret value** to view the value of the secret.

    1. Record the value of the **Secret Identifier** text box because you will use this later in the lab.

      > **Note**: You are recording the value of the **Secret Identifier** field, not the **Secret Value** field.

#### Task 3: Configure a Key Vault access policy

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securevault\*** Key Vault that you created earlier in this lab.

1.  In the **Key Vault** blade, select the **Access policies** link located in the **Settings** section.

1.  In the **Access policies** pane, select **+ Add Access Policy**.

1.  In the **Add access policy** blade, perform the following actions:

    1.  Select the **Select principal** link.

    1.  In the **Principal** blade, locate and select the service principal named **securefunc\[your name in lowercase\]**, and then select **Select**.

    1.  Leave the **Key permissions** list set to its default value.

    1.  In the **Secret permissions** drop-down list, select the **GET** permission.

    1.  Leave the **Certificate permissions** list set to its default value.

    1.  Leave the **Authorized application** text box set to its default value.

    1.  Select **Add**.

1.  Back in the **Access policies** pane, select **Save**.

1.  Wait for your changes to the access policies to be saved before you move forward with this lab.

#### Review

In this exercise, you created a server-assigned managed service identity for your function app and then gave that identity the appropriate permissions to get the value of a secret in your Key Vault. Finally, you created a secret that you will use within your function app.

### Exercise 3: Write function app code

#### Task 1: Create a Key Vault-derived application setting

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securefunc\*** function app that you created earlier in this lab.

1.  In the **Function Apps** blade, select the **Platform features** tab.

1.  In the **Platform features** tab, select the **Configuration** link located in the **General Settings** section.

1.  In the **Configuration** section, perform the following actions:

    1.  Select the **Application settings** tab.

    1.  Select **+ New application setting**.

    1.  In the **Add/Edit application setting** popup that appears, in the **Name** field, enter **StorageConnectionString**.

    1.  In the **Value** field, construct a value by using the following syntax: **@Microsoft.KeyVault(SecretUri=\<Secret Identifier\>)**

      > **Note**: You will need to build a reference to your **Secret Identifier** by using the above syntax. For example, if your Secret Identifier is **https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf**, then your value would be **@Microsoft.KeyVault(SecretUri=https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)**

    1.  Leave the **deployment slot setting** field set to its default value.

    1.  Select **OK** to close the popup and return to the **Configuration** section.

    1.  Select **Save** at the top of the blade to persist your settings.

1.  Wait for your application settings to persist before you move forward with the lab.

#### Task 2: Create a HTTP-triggered function

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securefunc\*** function app that you created earlier in this lab.

1.  In the **Function App** blade, click **+** next to the **Functions** drop-down.

1.  In the **New Azure Function** quickstart, perform the following actions:

    1.  Under the **Choose a Development Environment** header, select **In-Portal**.

    1.  Select **Continue**.

    1.  Under the **Choose a Function** header, select **More templates…**.

    1.  Select **Finish and view templates**.

    1.  In the list of templates, select **HTTP trigger**.

    1.  In the **New Function** pop-up, locate the **Name** text box and enter **FileParser**.

    1.  In the **New Function** pop-up, locate the **Authorization level** list and select **Anonymous**.

    1.  In the **New Function** pop-up, select **Create**.

1.  In the function editor, observe the example function script:

    ```cs
    #r "Newtonsoft.Json"

    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Primitives;
    using Newtonsoft.Json;

    public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
    {

        log.LogInformation("C# HTTP trigger function processed a request.");

        string name = req.Query["name"];

        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();

        dynamic data = JsonConvert.DeserializeObject(requestBody);

        name = name ?? data?.name;

        return name != null
            ? (ActionResult)new OkObjectResult($"Hello, {name}")
            : new BadRequestObjectResult("Please pass a name on the query string or in the request body");
    }
    ```

1.  **Delete** all the example code.

1.  Within the function editor, copy and paste the following placeholder function:

    ```cs
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        return new OkObjectResult("Test Successful");
    }
    ```

1.  Select **Save and run** to save the script and perform a test execution of the function.

1. The **Test** and **Logs** panes will automatically appear when the script executes for the first time.

1. Observe the **Output** text box in the **Test** pane. You should now see the value **Test Successful** returned from the function.

#### Task 3: Test the Key Vault-derived application setting

1.  Delete the existing code within the **Run** method of the script.

1.  The **Run** method should now look like this:

    ```cs
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

1.  Add the following line of code to get the value of the **StorageConnectionString** application setting by using the **Environment.GetEnvironmentVariable** method:

    ```cs
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  Add the following line of code to return the value of the **connectionString** variable by using the **OkObjectResult** class constructor:

    ```cs
    return new OkObjectResult(connectionString);
    ```

1.  The **Run** method should now look like this:

    ```cs
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        return new OkObjectResult(connectionString);
    }
    ```

1.  Select **Save and run** to save the script and perform a test execution of the function.

1.  Observe the **Output** text box in the **Test** pane. You should now see the connection string returned from the function.

#### Review

In this exercise, you securely used a service identity to read the value of a secret stored in **Azure Key Vault** and return that value as the result of an **Azure Function**.

### Exercise 4: Access Storage Account blobs

#### Task 1: Upload a sample storage blob

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securestor\*** storage account that you created earlier in this lab.

1.  In the **Storage account** blade, select the **Containers** link located in the **Blob service** section on the left side of the blade.

1.  In the **Containers** section, select **+ Container**.

1.  In the **New container** pop-up, perform the following actions:

    1.  In the **Name** text box, enter **drop**.

    1.  In the **Public access level** drop-down list, select **Blob (anonymous read access for blobs only)**.

    1.  Select **OK**.

1.  Back in the **Containers** section, select the newly created **drop** container.

1.  In the **Container** blade, select **Upload**.

1.  In the **Upload blob** pop-up, perform the following actions:

    1.  In the **Files** section, select the **Folder** icon.

    1.  In the File Explorer dialog box, go to **Allfiles (F):\\Allfiles\\Labs\\04\\Starter**, select the **records.json** file, and then select **Open**.

    1.  Ensure that **Overwrite if files already exist** is selected.

    1.  Select **Upload**.

1. Wait for the blob to be uploaded before you continue with this lab.

1. Back in the **Container** blade, select the **records.json** blob from the list of blobs.

1. In the **Blob** blade, view the blob metadata.

1. Copy the **URL** for the blob.

1. On the taskbar, right-select the **Microsoft Edge** icon and then select **New window**.

1. In the new browser window, navigate to the **URL** that you copied for the blob.

1. You should now see the **JSON** contents of the blob. Close the browser window showing the **JSON** contents.

1. Return to the browser window with the **Azure portal.**

1. Close the **Blob** blade.

1. Back in the **Container** blade, select **Change access level policy** located at the top of the blade.

1. In the **Change access level** pop-up that appears, perform the following actions:

    1.  In the **Public access level** drop-down list, select **Private (no anonymous access)**.

    1.  Select **OK**.

1. On the taskbar, right-select the **Microsoft Edge** icon and then select **New window**.

1. In the new browser window, navigate to the **URL** that you copied for the blob.

1. You should now see an error message indicating that the resource was not found.

    > **Note**: If you do not see the error message, your browser might have cached the file. Use **Ctrl+F5** to refresh the page until you see the error message.

#### Task 2: Pull the Storage Account SDK from NuGet

1.  On the navigation menu located on the left side of the portal, select the **Resource groups** link.

1.  In the **Resource groups** blade, locate and select the **SecureFunction** resource group that you created earlier in this lab.

1.  In the **SecureFunction** blade, select the **securefunc\*** function app that you created earlier in this lab.

1.  In the **Function App** blade, locate and select the existing **FileParser** function to open the editor for the function.

    > **Note**: You might need to expand the **Functions** option in the menu on the left side of the blade.

1.  On the right side of the editor, select **View files** to open the tab.

1.  In the **View files** tab, select **Add**.

1.  In the filename dialog that appears, enter **function.proj** and press Enter (displays an empty code editor).

1.  In the file editor, insert this configuration content:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netstandard2.0</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
            <PackageReference Include="Azure.Storage.Blobs" Version="12.0.0" />
        </ItemGroup>
    </Project>
    ```

1. In the editor, select **Save** button to persist your changes to the configuration.

    > **Note**: This **.proj** file contains the NuGet package reference necessary to import the [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.0.0) package.

1.  Select the **run.csx** file to return to the editor for the **FileParser** function.

1.  Minimize the **View files** tab.

    > **Note**: You can minimize the tab by selecting the arrow immediately to the right of the tab header.

1.  Within the editor, delete the existing code within the **Run** method of the script.

1.  At the top of the code file, add the following line of code to create a **using** directive for the **Azure.Storage** namespace:

    ```cs
    using Azure.Storage;
    ```

1.  At the top of the code file, add the following line of code to create a **using** directive for the **Azure.Storage.Blobs** namespace:

    ```cs
    using Azure.Storage.Blobs;
    ```

1.  Add the following line of code to create a **using** directive for the **Azure.Storage.Blobs.Models** namespace:

    ```cs
    using Azure.Storage.Blobs.Models;
    ```

1.  The **Run** method should now look like this:

    ```cs
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

#### Task 3: Write storage account code

1.  Add the following line of code within the **Run** method to get the value of the **StorageConnectionString** application setting by using the **Environment.GetEnvironmentVariable** method:

    ```cs
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  Add the following line of code to create a new instance of the **BlobServiceClient** class by passing in your *connectionString* variable to the constructor:

    ```cs
    BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
    ```

1.  Add the following line of code to use the **BlobServiceClient.GetBlobContainerClient** method, while passing in the **drop** container name to create a new instance of the **BlobContainerClient** class that references the container that you created earlier in this lab:

    ```cs
    BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
    ```

1.  Add the following line of code to use the **BlobContainerClient.GetBlobClient** method, while passing in the **records.json** blob name to create a new instance of the **BlobClient** class that references the blob that you uploaded earlier in this lab:

    ```cs
    BlobClient blobClient = containerClient.GetBlobClient("records.json");
    ```

1.  The **Run** method should now look like this:

    ```cs
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
    }
    ```

#### Task 4: Download a blob

1.  Add the following line of code to use the **BlobClient.DownloadAsync** method to download the contents of the referenced blob asynchronously and store the result in a variable named *response*:

    ```cs
    var response = await blobClient.DownloadAsync();
    ```

1.  Add the following line of code to return the various content stored in the *content* variable by using the **FileStreamResult** class constructor:

    ```cs
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

1.  The **Run** method should now look like this:

    ```cs
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
        var response = await blobClient.DownloadAsync();
        return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    }
    ```

1.  Select **Save and run** to save the script and perform a test execution of the function.

1.  Observe the **Output** text box in the **Test** pane. You should now see the content of the **$/drop/records.json** blob stored in your **storage account**.

#### Review

In this exercise, you used C\# code to access a Storage Account securely and then download the contents of a blob.

### Exercise 5: Clean up subscription

#### Task 1: Open Azure Cloud Shell and list resource groups

1.  In the top navigation bar in the Azure Portal, select the **Cloud Shell** icon to open a new shell instance.

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

#### Task 2: Delete resource group

1.  In the prompt, type the following command and press Enter to delete the **SecureFunction** resource group:

    ```powershell
    az group delete --name SecureFunction --no-wait --yes
    ```

1.  Close the **Cloud Shell** pane at the bottom of the portal.

#### Task 3: Close active application

> Close the currently running **Microsoft Edge** application.

#### Review

In this exercise, you cleaned up your subscription by removing the **resource groups** used in this lab.
