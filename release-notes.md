## Version 1.0.0

Initial release of Listener.

#### Known Issues

* *B1114*
  * *Description* - Normal users can create/update targets through API. Should be limited to only Admins.
  * *Workaround* - None
* *B1116*
  * *Descrption*​ - Admins can update LDAP settings through API. Should be limited to Listener Super User.
  * *Workaround*​ - None
* *B1165*
  * *Description*​ - Any user is able to start and pause any system target using API. Should be limited to target owners and Admins.
  * *Workaround*​ - None
* *B1113*
  * *Description*​ - Proper time is not stored in API responses for `created_at` and `updated_at` timestamps.
  * *Workaround*​ - None
* *B925*
  * *Description*​ - Starring a source ignored if volumetric data still loading.
  * *Workaround*​ - Wait until source volumetrics are displayed (no spinner on graph) before staring a source.
