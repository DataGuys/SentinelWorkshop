# Module 6 - Lab 1 - Exercise 2 - Connect Windows devices to Azure Sentinel using data connectors

### Task 1: Create a Windows Virtual Machine in Azure.

In this task, you will create a Windows virtual machine.

1. Login to WIN1 virtual machine as Admin with the password: **Pa55w.rd**.  

2. In the Edge browser, navigate to the Azure portal at https://portal.azure.com.

3. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

4. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

5. Select **Create a Resource**.

6. In the **search the Marketplace** box, enter *Windows 10*. 

7. Select the **Create** dropdown for Microsoft Windows 10.  Then select **Windows 10 Enterprise, version 20H2**.

8. Select your Subscription.

9. Create a new Resource Group named **rg-AZWIN01** if you have not done so already.

**Note:** This needs to be a new resource group.  You are going to delete the Virtual machine after the exercise.  

10. Set the Virtual Machine name to AZWIN01.

11. Set the Region to the appropriate region for your area.  The appropriate region may default.

12. Enter a Username of your choosing that is acceptable for Azure.

13. Enter a Password of your choosing. 

**Hint:** It might be easiest to use your tenant password.

14. Select Licensing confirmation.

15. Select **Review + Create**.

16. Select **Create**. Wait for the Resource to be created, this may take a few minutes.

### Task 2: Connect an Azure Windows VM.

In this task, you will connect an Azure Windows virtual machine to Azure Sentinel.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Azure Sentinel**.

2. Select your Azure Sentinel Workspace you created earlier.

3. From the Data Connectors Tab, select the **Security Events** connector from the list.

4. Select your Azure Sentinel Workspace if prompted.

5. Select **Open connector page** on the connector information blade.

**Note:** The instructions for Install agent on a Windows Virtual Machine and Install agent on a non-Azure Windows Machine may be reversed.  The links take you to the proper location even with the reversed text.

6. Select the **Install agent on a Windows Virtual Machine** option.

7. Select **Download & install agent for Azure Windows Virtual machines**.

8. Select the **AZWIN01** virtual machine in the list that you just created in the previous step, then select **Connect**. Wait until the connecting message disappears.

9. Select **Virtual machines** in the navigation list. You should now see the machine is connected.

**Note:** The virtual machine is only used in this task.  

10. In the Azure portal search, enter *resource groups*.  Select **Resource Groups**.

11. Select **rg-AZWIN01** from the list.

12. Select **Delete resource group** from the command bar.

13. Enter **rg-AZWIN01** into the "Are you sure you want to delete" pane, then select **Delete**.

### Task 3: Connect a non-Azure Windows Machine.

In this task, you will connect a non-Azure Windows virtual machine to Azure Sentinel.

1. Login to WIN2 virtual machine as Admin with the password: **Pa55w.rd**.  

2. Open the browser, search for, download, and install the new Microsoft Edge browser. Start the new Edge browser.

3. Open a browser and log into the Azure Portal at https://portal.azure.com with your credentials.

4. In the Search bar of the Azure Portal, type *Sentinel*, then select **Azure Sentinel**.

5. Select your Azure Sentinel Workspace.

6. From the Data Connectors tab, select the **Security Events** connector from the list.

7. Select **Open connector page** on the connector information blade.

8. In the Select which events to stream area, select **All Events**, then select **Apply Changes**.

9. Select the **Install agent on a non-Azure Windows Virtual Machine**.

**Note:** The instructions for Install agent on a Windows Virtual Machine and Install agent on a non-Azure Windows Machine may be reversed. The links take you to the proper location even with the reversed text.

10. Select **Download & install agent for non-Azure Windows Virtual machines**. 

11. Select the link for **Download Windows Agent (64 bit)**.

12. Run the .exe file that is downloaded and confirm and User Account Control prompt that may appear.

13. Select **Next** on the Welcome dialog.

14. Select **I Agree** on the Microsoft Software License Terms page.  On the Destination prompt select **Next**.

15. On the Agent Setup Options prompt, select **Connect the agent to Azure Log Analytics (OMS)** option, then select **Next**.

16. In the browser, copy the **Workspace ID** from the Agents Management page and paste into the Workspace ID in the dialog. 

17. In the browser, copy the **Primary key** from the Agents Management page and paste into the Primary key in the dialog. 

18. Select **Next**.

19. Select **Next** on the Microsoft Update page.

20. Then select **Install**.

### Task 4: Install and collect Sysmon logs.

In this task, you will install and collect Sysmon logs.

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. In the browser, go to https://docs.microsoft.com/sysinternals/downloads/sysmon

2. Download Sysmon from the page by select **Download Sysmon**.

3. Open the downloaded file and extract the files to a new directory c:\sysmon

4. In the Windows Taskbar for WIN2 search box, enter *command*.  The search results will show command prompt app.  Right-click on the command prompt app and select **Run as Administrator**.  Confirm any User Account Control prompts that appear.

5. Enter *cd \sysmon*

6. type *notepad sysmon.xml* to create a new file.

7. Open a tab in the browser and navigate to: https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

8. Copy the contents of that file from Github to the sysmon.xml notepad file you just create and save the file.

9. In the command prompt type the following and press enter:
    sysmon.exe -accepteula -i sysmon.xml

10. In the browser, navigate to the Azure portal at https://portal.azure.com 

11. In the Search bar of the Azure portal, type *Sentinel*, then select **Azure Sentinel**.

12. In Azure Sentinel, select **Settings** from the Configuration area and then select **Workspace settings** tab.

13. Make sure your Azure Sentinel Workspace is selected.

14. Select **Agents configuration** in Settings.

15. Select the **Windows Event logs** tab.

16. Select **Add windows event log** button.

17. Enter **Microsoft-Windows-Sysmon/Operational** in the Log name field.

18. Select **Apply**.

### Task 5: Onboard Microsoft Defender for Endpoint Device.

In this task, you will on-board a device to Microsoft Defender for Endpoint.

**Note:** If you completed the labs in the first module of this course you have already performed this task.  If you’re using the same virtual machine from that lab exercise you don’t need to do this task.

1. Login to WIN1 virtual machine as Admin with the password: **Pa55w.rd**.  

2. Go to the Microsoft Defender Security Center at (https://securitycenter.microsoft.com) and login with the **Tenant Email** credentials if you are not currently in the portal.

3. Select **Settings** from the left menu bar.

4. Select **Onboarding** in the Device management section.

5. Select **Download Package**.

6. Extract the downloaded .zip file.

7. Run the Windows Command Prompt as **Administrator** and agree to any User Account Control prompts that appear.

8. Run the WindowsDefenderATPLocalOnboardingScript.cmd file that you just extracted as administrator. **Note** By default the file should be in the c:\users\admin\downloads directory. Answer Y to questions presented by the script. 

9. From the Onboarding page in the Microsoft Defender Security Center portal, copy the detection test script and run in the open **Administrator: Command Prompt** window.

10.  In the Microsoft Defender Security Center portal menu, select **Devices inventory** icon from the left navigation. You should now see your device in the list. **Note** It can take up to 5 minutes for the device to be displayed in the portal.

## Proceed to Exercise 3
