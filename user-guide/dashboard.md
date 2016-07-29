When you log in, Listener takes you to the **Dashboard** and navigation panel. From the **Dashboard** and navigation panel, you can perform the following tasks:

- View starred source activity
- Access source details
- Open a list of all data sources
- View records and latency information for all sources
- View sources with the most data
- Create a source
- Access administrator (ADMIN) settings, if you have administrative privileges

## Source Activity

The **Source Activity** card collection shows the latest activity from all starred sources for the selected time period. When you create a source, Listener stars it automatically and displays it in the **Dashboard**. For information about managing sources, including starring and unstarring sources, see [Manage Sources](manage-sources.md).

Time periods include the following:

- **1H** (1 Hour)
- **1D** (1 Day)
- **7D** (7 Days)
- **1M** (1 Month)

The default time period is **1H**.

**Note:** If a source card displays the message **No data for selected range**, view the **Source** details for more information.

### Filtering Source Activity by Time Period

1. In the **Source Activity** header, click the desired tab (**1H**, **1D**, **7D**, or **1M**).

### Viewing a Snapshot of Source Size and Records 

1. Under **Source Activity**, mouse over a specific time or date in a source's card. 

### Accessing Source Details
**Source** details include the following:

 * Targets
 * Ingest Code Samples
 * Owners
 * Description
 * Source Secret Key 

1. Click anywhere in the source's card.
2. [Optional] To unstar this source, click the star button above **Source Info**. Click it again to restar the source.
2. To return to the **Dashboard**, click **Dashboard** in the navigation panel.

The **Source** details card provides options for creating a new target, starring a source, and editing a source. For more information, see [Create a Target](create-target.md) or [Manage Sources](manage-source.md).

### Accessing a List of All Data Sources

The ** Data Sources** card collection lists all data sources, starred and unstarred. It provides options for sorting and filtering sources and creating new sources. 

1. Do one of the following:

 * At the bottom of the **Source Activity** list, click **VIEW ALL**.
 * In the navigation panel, click **Data Sources**. 

2. [Optional] To unstar a source, click the star button next to the source's name. Click it again to restar the source.
3. To return to the **Dashboard**, click **Dashboard** in the navigation panel.

For more information about the list of **Data Sources**, see [Data Sources](data-sources.md).

## All Sources

The **All Sources** card collection shows total activity from all sources, starred and unstarred, for the selected time period. Listener presents total activity in the following cards: 

* **Total Records & Size**
* **Router Latency**

Time period options include the following:

- **1H** (1 Hour)
- **1D** (1 Day)
- **7D** (7 Days)
- **1M** (1 Month)

The default time period is **1H**. 

### Filtering Activity from All Sources by Time Period

1. In the **All Sources** header, click the desired tab (**1H**, **1D**, **7D**, or **1M**). Listener applies that time period to both the **Total records & Size** and **Router Latency** cards.

### Viewing a Snapshot of Total Records and Size or Router Latency 

1. In the **Total Records & Size** or **Router Latency** card, mouse over a specific time or date. 

### Viewing a List of All Data Sources

The ** Data Sources** card collection lists all data sources, starred and unstarred. It provides options for sorting and filtering sources and creating new sources. 

1. Under **All Sources**, click anywhere in the **Total Records & Size** or **Router Latency** card.
2. To return to the **Dashboard**, click **Dashboard** in the navigation panel.

## Most Data

The **Most Data** card collection lists sources with the most data for the selected time period, by **Volume** or by **Records**. 

Time period options include the following:

- **1H** (1 Hour)
- **1D** (1 Day)
- **7D** (7 Days)
- **1M** (1 Month)

The default time period is **1H**. 

The default display option is by **Volume**.

**Note:** If a source card displays the message **No data for selected range**, view the **Source** details for more information.

### Filtering Sources with the Most Data by Time Period

1. In the **Most Data** header, click the desired tab (**1H**, **1D**, **7D**, or **1M**). Listener applies that time period to all source cards under **Most Data**.

### Filtering Sources with the Most Data by Records or Volume

1. In the **Most Data** header, click the desired option (**Records**or **Volume**). Listener applies that option to all source cards under **Most Data**.

### Viewing Source Details

**Source** details include the following:

 * Targets
 * Ingest Code Samples
 * Owners
 * Description
 * Source Secret Key 

1. Under **Most Data**, click anywhere in a source's card.
2. To return to the **Dashboard**, click **Dashboard** in the navigation panel.

The **Source** details card provides options for creating a new target, starring a source, and editing a source. For more information, see [Create a Target](create-target.md) or [Manage Sources](manage-sources.md).

## Creating a Source

Create a source from the **Dashboard**, **Data Sources**, or **Manage Sources**. For more information, see [Create a Source](create-source.md).

## Accessing ADMIN Settings

Only users with administrative privileges will see the following **ADMIN** settings in the navigation panel:

**Manage Sources**

Add, lock, edit, and delete sources. For more information, see [Manage Sources](manage-sources.md).

**Manage Systems**

Add, edit, and delete systems. For more information, see [Manage Systems](manage-systems.md).

**Manage Targets**

Add, activate, lock, edit, and delete targets. Set up batch mode by time or number of records, and configure target mapping. For more information, see [Manage Targets](manage-targets.md).

**Manage Users**

Edit and delete users. Promote users to and demote users from administrative status. For more information, see [Manage Users](manage-users.md).

**Logs**

View user activity and system errors. Use the filter options to narrow the results. For more information, see [Logs](logs.md).

**Status**

View status of and restart **System Services**, and view agent resources. For more information, see [Status](status.md).

**Update**

View and update the current version of Listener or rollback to a previous version. For more information, see [Update](update.md).

**Settings**

Change **LDAP Authentication** settings and **System Password**. For more information, see [Settings](settings.md).
