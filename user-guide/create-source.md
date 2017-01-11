Create sources from the **Dashboard** or **Data Sources** card.

If you are using LDAP, Listener associates each source with an owner or owners. You must have at least one owner for each source. The user who creates a source is the default owner and can add and delete other owners. All owners can modify or delete the source and all associated targets.

1. From the **Dashboard** or **Data Sources**, click the blue floating action button.
2.  Under **Source Name**, enter a name, up to 100 characters. For example: `Corporate Website`
3.  Under **Source Description**, enter a description, up to 5000 characters. For example: `Clickstream data from our corporate website`
4. Select the **Source Type**.
 * To send messages to RESTful sources using the [Ingest API](../api/vi/sources.md), select **REST**.
 
5. [Optional] If Listener is using LDAP, do either of the following:
 * To add additional owners, click the **Owner(s)** box, start typing the user's LDAP username, and click the username when it appears.
 * To remove yourself or another owner, click the delete button next to the owner name.
6. Click **Save**. 

When you create a source, Listener automatically stars it, making it a favorite, and displays it in the **Source Activity** card on the **Dashboard**. You can unstar a source and remove it from the **Dashboard**. For more information about unstarring and starring sources, see [Data Sources](data-sources.md).

## Data Ingest Alert

When you create a **REST** source, Listener is not ingesting data yet and an ingest alert appears in the **Dashboard**. For information about using the Source Secret Key to stream data from the source to Listener, see [Ingest Authorization](../ingest/index.md#authorization)

## Ingest Code Samples
* [cURL](samples-ingest/curl.md)
* [Java](samples-ingest/java.md)
* [Python](samples-ingest/python.md)
