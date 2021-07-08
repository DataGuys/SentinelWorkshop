# Module 7 - Lab 1 - Exercise 3 - Create a Scheduled Query

### Task 1: Create a Scheduled Query.

In this task, you will create a scheduled query.

1. Log in to WIN1 virtual machine as Admin with the password: **Pa55w.rd**.  

2. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

3. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

4. In the Search bar of the Azure portal, type *Sentinel*, then select **Azure Sentinel**.

5. Select your Azure Sentinel Workspace.

6. Select **Analytics** from the Configuration area.

7. Select the **Create** button, and select **Scheduled query rule**.

8. On the General tab, enter the Name *Inactive Account sign in attempts*.

9. For Tactics, select **Initial Access**.

10. For Severity, select **Medium**

11. Select **Next : Set rule logic >** button:

12. For the rule query, paste in the following KQL statement:

```KQL
SigninLogs
| where ResultType == "50057"
| where ResultDescription =~ "User account is disabled. The account has been disabled by an administrator."
| summarize StartTimeUtc = min(TimeGenerated), EndTimeUtc = max(TimeGenerated), count(), applicationCount = dcount(AppDisplayName), 
applicationSet = makeset(AppDisplayName) by UserPrincipalName, IPAddress
| extend timestamp = StartTimeUtc, AccountCustomEntity = UserPrincipalName, IPCustomEntity = IPAddress
```

**Warning:** When using the Paste function to the virtual machine.  Extra | (pipe) characters could be added.  Make sure what is pasted looks like the following KQL statement.

**Note:** If you select the link to "View query results", you should not receive any results.  You should also not receive an error.  

13. Review the Map entities.  The entities are shown as mapped in the query because the query output includes fields:

timestamp = StartTimeUtc, AccountCustomEntity = UserPrincipalName, IPCustomEntity = IPAddress

14. Back in the Analytics rule wizard - Create new rule blade in the Query scheduling area, enter **5** and select **Minutes** for the Run query every option.

15. In the Query scheduling area, enter **1** and select **Days** for the Lookup data from the last option.

16. For the Alert threshold area, leave the options unchanged.

**Note:** Best practices are to manage thresholds in the alert rule KQL query statement.

17. For the Event grouping area, leave the **Group all events into a single alert** as the selected option.

18. Select the **Next: Incident settings** button.  

19. On the Incident settings tab, review the default options.

20. Select the **Next: Automated response** button.

21. On the Automated response tab, select the playbook Post-Message-Teams you had previously created.

22. Select the **Next: Review** button.
  
23. Select **Create**.

### Task 2: Test our new rule.

In this task, you will create a test your new scheduled query rule.

1. In the Search bar of the Azure portal, type *Azure Active Directory*. Then select **Azure Active Directory**.

2. Select **Users** in the Manage area.

3. Select User **Christie Cline** in the list. The Christie Cline | Profile page is displayed.

4. Select **Edit**.

5. In the settings area, change **Block sign in** to **Yes**.

6. Now select **Save** from the Command bar.

7. In the Azure portal, select the user avatar at the top right and sign out.

8. Close your browser.

9. Open a browser and navigate to https://portal.office.com and try to login with user ChristieC@**Tenant Email domain** and password should be the same as your admin's tenant password.  You should receive a warning that your account has been locked.

10. Close your browser. Wait 10 minutes for the alert to process.

11.  In the Edge browser, go to the Azure portal at https://portal.azure.com.

12. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider for Admin user and then select **Next**.

13. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider for Admin user and then select **Sign in**.

14. In the Search bar of the Azure portal, type *Sentinel*, then select **Azure Sentinel**.

15. Select your Azure Sentinel Workspace.

16. Select the **Incidents** menu option.

17. You should see the newly created Incident.  Select the Incident and review the information in the right blade.

18. Open Microsoft Teams. Goto your *SOC* Team, ... and see the message post about the incident.

## Proceed to Exercise 4
