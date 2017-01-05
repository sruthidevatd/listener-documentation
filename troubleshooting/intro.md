Use these guidelines for troubleshooting common problems:

## Administration

__Problem__:
User cannot log into Listener.

__Solution__:
Ensure corporate LDAP group settings are correct in **ADMIN > Settings > LDAP**, and user is a member of an included LDAP group.

---
__Problem__:
Browser complains about insecure SSL/TLS certificate.

__Solution__:
Ensure Listener-installed SSL/TLS certificate is issued by a trusted certificate provider, not self-signed or expired.

---
__Problem__:
Admin cannot log into **Settings**.

__Solution__:
Only the super-user Admin is allowed access to Listener **ADMIN** > **Settings**.  User-level admins do not have this privilege.

__Problem__:
Unable to add LDAP settings.

__Solution__:
Ensure the username and password are valid. Listener requires original credentials to verify settings.

---
__Problem__:
Cannot find location to add new users to Listener.

__Solution__:
Users are automatically added to listener the first time they log in.  User restriction occurs at the LDAP group level.

## API
__Problem__:
A deleted item still appears in API.

__Solution__:
To allow for Elasticsearch index refreshing, wait at least 1 second after deletion to confirm the item has been deleted.

## Data Ingestion

__Problem__:
Ingest API returns the `201` status code, but data does not appear to be landing.

__Solution__:
Send a test packet with Header `Sync=1` and see if UUID is returned with the `201` status code.

---
__Problem__:
When writing to Teradata, data is not inserted, and the following error message appears: `Bad parameter type, could not bind`

__Solution__:
Ensure Teradata column datatype is `varchar,` `json,` or `clob.`  Currently, these are the only supported datatypes for Teradata.

---
__Problem__:
When writing to Aster, data is not inserted and the following error message appears: `Bad parameter type, could not bind`

__Solution__:
Ensure Aster data column datatype is `varchar` or `text.`  Currently, these are the only supported datatypes for Aster.

---
__Problem__:
When using `/messages` endpoint and sending an array of JSON docs, target table has a single character as each message/record.

__Solution__:
This occurs when the JSON array is invalid. Ensure the JSON array is valid.

---
__Problem__:
Ingest Services does not deploy properly and throws a `503` error.

__Solution__:
When Ingest starts, it checks for sources in Elasticsearch and throws an error if it does not find any sources. Create a source and restart Ingest. 

## MQTT
__Problem__:
Messages are not getting to the source.

__Solution__:
Ensure the topic is valid.

__Problem__:
State of the source indicates a bad broker.

__Solution__:
Check for network blocks from MQTT to listener.

## Sources

__Problem__:
Dashboard is empty after user created sources.

__Solution__:
Sources must be starred to appear on the Dashboard.

---
__Problem__:
The following error message appears: `{"title":"Could not save this source","content":"Data validation error: Owner attribute is required"}`

__Solution__:
Log out and log back into Listener.

## Systems
__Problem__:
User does not have access to add a target system (Teradata, Aster, HDFS, or HBase).

__Solution__:
Ensure the user has Admin privileges.  Only Admins are allowed to add systems to Listener, which can then be selected by non-admin users to create targets.

---
__Problem__:
Admin cannot add or verify an HDFS system.

__Solution__:
Ensure the URL/IP is prefaced by `hdfs://` and ends with the `:port-number.`

---
__Problem__:
Admin cannot validate and save a new system.

__Solution__:
Ensure autofill is turned off in the browser.

## Targets
__Problem__:
Data is not inserted into the target system.

__Solution__:
Ensure user credentials supplied have proper privileges to access and insert data on the target system. 

---
__Problem__:
Cannot retrieve column data from Teradata after checking valid target credentials.

__Solution__:
Ensure user has proper privileges for `getColumnPrivileges` and `getColumn` on the Teradata system:

```
Select access on DBC.Tables[V][X]
Select access on DBC.Columns[V][X]
Select access on DBC.AllRights[V][X]
Select access on DBC.UDTInfo
```
---
__Problem__:
When creating an HDFS target, the following message appears: `Error while creating table`

__Solution__:
Ensure Hcatalog is set up correctly and that port 50111 is open to Hcatalog.

---
__Problem__:
Target is stuck in deploy mode.

__Solution__:
Ensure there are enough resources to deploy a new target.

---
__Problem__:
Admin cannot add a target in the **Manage Targets** view.

__Solution__:
Ensure at least one source exists in Listener, and that source is selected in the target form.

---
__Problem__:
Connection to a websocket target fails and the following message appears: `503 Service Unavailable`

__Solution__:
Reattempt the websocket connection until a successful connection is made.

## Writer

__Problem__:
When transactions such as `insert` or `delete` are run on a Teradata table by anyone other than Listener, writer errors out because of deadlock. User cannot find any new data in the target table.

__Solution__:
If you want to modify data while listener is writing, use partition tables instead of regular tables.

__Problem__:
Insert query fails because of  datatype mismatch, and the following error message appears in the **Manage Targets** view under the target name: `Target error` 

__Solution__:
Click **VIEW ERROR DETAILS** under the target error message for more information.
