Only users with administrative privileges will see **Logs** and other **ADMIN** options in the navigation panel.

From the **Logs** view, you can perform the following tasks:

- Specify the number of logs to appear on a page
- View all user actions
- Filter the user log by action type
- Filter the user log by user name
- Filter the user log by successful or failed actions
- View all system errors
- Filter the system error log by type (Mesos or Zookeeper)
- Search for a system error by term
- Export the system error log (all or filtered)

**Note**: You can combine filtering options in **USER AUDIT LOGS** and **SYSTEM ERROR LOGS**.

## Viewing Logs

1. In the **ADMIN** navigation panel, click **Logs**.
 
### Specifying the Number of Logs to Appear on a Page

The default setting for number of logs per page is 100. You can change this in the **USER AUDIT LOGS** and **SYSTEM ERROR LOGS** tabs. Listener maintains this setting while you are in the tab. When you leave the tab, Listener reverts to the default setting.

1. In the lower right of the **USER AUDIT LOGS** or **SYSTEM ERROR LOGS** page, in the **Per Page** list, select the number of logs you want to appear on the page while viewing that tab (**100**, **500**, **1000**, or **5000**).

## USER AUDIT LOGS

**USER AUDIT LOGS** is the default view and lists user activity on individual cards. Each card shows the user name, action taken, status of the action (**success** or **failed**), and a timestamp.

### Filtering the User Log by Action Type

1. In the **Filter by action** list, select one of the following filters:
 * **Add**: Lists only sources, systems, or targets added
 * **Update**: Lists only sources, systems, or targets updated
 * **Delete**: Lists only sources, systems, or targets deleted
 * **Star**: Lists only sources that have been starred
 * **Unstar**: Lists only sources that have been unstarred
 * **Login**: Lists only failed login attempts

2. To clear this filter, select the delete button next to the filter box.

### Filtering the User Log by User Name

1. In the **Filter by user** box, start typing any part of the user name.
2. When the desired user name appears under the box, click it.
3. To clear this filter and view logs for all users, delete the characters you typed in the **Filter by user** box.

### Filtering the User Log by Successful or Failed Actions

**All Actions** is the default filter.

1. In the action list, select one of the following filters:
 * **Successful**
 * **Failed**
2. To clear this filter, select **All Actions**.

## SYSTEM ERROR LOGS

**SYSTEM ERROR LOGS** lists all system error messages from Mesos and Zookeeper.

### Filtering the Error Log by Type

1. In the **Filter by type** list, select **Mesos** or **Zookeeper**.
2. To clear this filter and view logs for both types, select **All**.

## Searching for Errors by Term

1. In the **Search by term** box, start typing any part of the term. Listener automatically filters the list as you type.
2. To clear this search and view all errors, delete the characters you typed in the **Search by term** box.

## Exporting System Error Logs for Support

1. [Optional] Use the filter and search options to narrow the list of logs for export.
2. Next to **Search by term**, click the download arrow button. Listener displays the error logs in a new browser window. 
3. Use your browser's save feature to save the file to your system. 

**Tip:** If your browser does not suggest a specific file type when you attempt to save it, assign the json extension. For example: `error.json`
