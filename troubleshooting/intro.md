This guide contains troubleshooting solutions for common problems.

## Targets
__Problem__:
Data is not inserted into the target system.

__Solution__:
Ensure user credentials supplied have proper privileges to access and insert data on the target system. 

---
__Problem__:
Cannot retrieve column data from Teradata after checking valid target credentials.

__Solution__:
Ensure user has proper privileges for `getColumnPrivileges`
and `getColumn` on the Teradata system:

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
Admin cannot add a Target in the Manage Targets view.

__Solution__:
Ensure at least one Source exists in Listener, and that source is selected in the Target form.

## Sources
__Problem__:
Dashboard is empty after the user created sources.

__Solution__:
Sources must be starred to appear on the Dashboard.

---
__Problem__:
The following error message appears: `{"title":"Could not save this source","content":"Data validation error: Owner attribute is required"}`

__Solution__:
Log out and log back into Listener.

## Systems
__Problem__:
User does not have access to add a target Teradata, Aster, HDFS, or HBase system.

__Solution__:
Ensure the user has admin privileges.  Only admins are allowed to add systems to Listener, which can then be used by non-admins.

---
__Problem__:
Admin can't add or verify an HDFS system.

__Solution__:
Ensure the url/IP is prefaced by `hdfs://` and ends with the `:port-number`.

---
__Problem__:
Admin cannot validate and save a new system.

__Solution__:
Ensure autofill is turned off in the browser.


## Data Ingestion
__Problem__:
Ingest API returns the `201` status code, but data does not appear to be landing.

__Solution__:
Send a test packet with Header `Sync=1` and see if UUID is returned with the `201` status code.

---
__Problem__:
When writing to Teradata, data is not inserted, and the following error message appears: `Bad parameter type, could not bind`

__Solution__:
Ensure Teradata column datatype is `varchar`, `json`, or `clob`.  Currently, these are the only supported datatypes for Teradata.

---
__Problem__:
When writing to Aster, data is not inserted, and the following error message appears: `Bad parameter type, could not bind`

__Solution__:
Ensure Aster data column datatype is `varchar` or `text`.  Currently, these are the only supported datatypes for Aster.

## Administration
__Problem__:
User can not log into Listener.

__Solution__:
Ensure corporate LDAP group settings are correct in _ADMIN > Settings > LDAP_, and user is a member of an included LDAP group.

---
__Problem__:
Browser complains about insecure SSL/TLS certificate.

__Solution__:
Ensure Listener-installed SSL/TLS certificate is issued by a trusted certificate provider, not self-signed or expired.

---
__Problem__:
Admin cannot log into _Settings_.

__Solution__:
Only the super-user Admin is allowed access to Listener _ADMIN > Settings_.  User-level admins do not have this privilege.

---
__Problem__:
Cannot find location to add new users to Listener.

__Solution__:
Users are automatically added to listener the first time they log in.  User restriction occurs at the LDAP group level.

## API
__Problem__:
A deleted item still appears in API.

__Solution__:
To allow for ES index refreshing, wait at least 1 second after deletion to confirm the item has been deleted.
