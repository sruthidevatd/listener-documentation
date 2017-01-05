## Version 01.01.00.424
#### New for Listener v1.1
* Introducing installation support for Listener on AWS in addition to Openstack.
* New Broadcast Streams functionality is available as a source data distribution end-point.  The Broadcast Streams features generates a web socket with a unique URL and authentication token so you can send your streaming source data in near real-time to stream processing engines like Spark.
* Dashboard includes a new "Most Data" view that displays the top five most volume or records on the platform.
* View more information about the Listener deployment with an improved administrator status page that now includes status for Writers, Listener Services, Agent Resources.
* New and improved filters for administrators on the Mange Targets view and for users on the Sources view.
* Code samples are always available in the source view.
* New installation process - please go to http://docs.uda.io for more information.

#### Features
* Easy to navigate web app user interface (UI) based on material design.
* Powerful user web app with a dashboard to monitor all your real-time data in one view.
* Create and view sources for real-time ingestion via UI and RESTful APIs.
  * Authenticated users can create data sources.
  * Authenticated users can view/find/search/favorite/co-own data sources.
  * Data can be sent in any format.
  * Supports single record or multiple record data, up to 1MB per record.
  * Listener will provide acknowledgement of receipt of data.
  * Map metadata and data to specific columns in target (for TD and Aster).
  * Owners of the data source can lock the target and data source from changes
  * Monitor volume metrics (record size and count) per source over a day, hour, week or month.
* Write source data to UDA and real-time targets via UI or RESTful APIs.
  * Owners of a data source can add one or more targets (using pre-configured Systems.)
  * Support writing data in real-time, batch by records, and batch by time to the UDA.
  * Support writing data in real-time as Broadcast Streamers for 3rd party systems and complex event processors.
  * Guaranteed delivery; at-least once semantics.
  * Prebuilt backpressure support for ingestion spikes and retention policies.
  * Pausing/resuming of writing to targets.
  * Monitor latency metrics of each source target(s) over a day, hour, week or month.
* Administrator role capabilities via UI and RESTful APIs.
  * Security controls include LDAP integration for authentication, security.
  * Provide roles for administrator, user and source owner.
  * OAUTH2 authentication for services.
  * Monitor and manage system targets and all user sources and associated targets.
  * Monitor and manage the platform and system services.
  * Generates email alerts for target error or service failures (if SMTP provided via API.)

#### Requirements
* Tested on the following systems:
 * Hadoop 2.3 - 2.6 (CDH 5.2+, HDP 2.3+)
 * Aster 6.20+
 * Teradata 15.10+
 * Hbase 1.1.2+
* For general requirements, go to: http://docs.uda.io/installation/prerequisites.html
* For Openstack requirements, go to: http://docs.uda.io/installation/openstack.html
* For Amazon Web Services requirements, go to: http://docs.uda.io/installation/aws.html

#### Known Limitations
* Licensing in Admin screen is disabled.  Listener licensing will activate in a future update.
* Teradata and Aster tables must be created prior to using Listener.
* No Kerberos for HDFS/Hadoop
* Support Systems and Writer Configurations - http://docs.uda.io/user-guide/supported-systems.html
* Listener scaling/sizing must be defined at install time.
* Data duplication may occur. Listener will support exactly once semantics in a future update.

#### Errata and Known Bugs

* 1113 - Proper time is not returned in API responses.
* 1358 - Email alerts contain broken links.


## Version 01.00.06

### Enhancements

* Dashboard includes new "Most Data" card that displays the top five, most Volume or most Records on the platform.
* Status page for Admins provides more information about the Listener deployment, including status for Writers, Listener Services, and Agent Resources.
* Manage Tagets view provides new and improved filters for Admins.
* Data Sources view provides new and improved filters for all users.
* Source view always includes code samples.

### Fixes

* Fixed - 1345 - Listener will not automatically validate column mapping datatype.
* Fixed - 1421 - Writers do not shut down properly during system update.
* Fixed - 1472 - Removed the Trash icon in Admin Menu > Manage Users.
* Fixed - 1429 - Starring a source will not retain the star in UI and API.
* Fixed - 1528 - writer/router does not startup properly when Elastic service is not available.
* Fixed - 1554 - App & Installer services fails to startup correctly if there is a connection error.
* Fixed - 1226,1227,1228 - credentials in target fields are not encrypted inside application.
* Fixed - 1421 - Writer/Router services will shutdown before an update.
* Fixed - 1574 - Aster database and schema must be the same value for Aster writer to deploy in Listener.
* Fixed - 1568 - Unsupported data type for the Aster JDBC driver will cause the writer to crash.
* Fixed - 1492 - Router Latency (Firehose to Streams) Chart - Latency (Y-Axis) has rounding error when latency at less than 1ms.
* Fixed - 1576 - Fails to validate hbase Cf/table on HDP.

### Features

* Easy-to-navigate web app user interface (UI) based on material design.
* Powerful user web app with a dashboard to monitor all your real-time data in one view.
* Create and view sources for real-time ingestion via UI and RESTful APIs.
  * Authenticated users can create data sources.
  * Authenticated users can view/find/search/favorite/co-own data sources.
  * Data can be sent in any format.
  * Supports single-record or multiple-record data, up to 1 MB per record.
  * Listener provides acknowledgement upon receipt of data.
  * Map metadata and data to specific columns in target (for TD and Aster).
  * Owners of the data source can lock the target and data source from changes.
  * Monitor volume metrics (record size and count) per source over a day, hour, week, or month.
* Write source data to UDA targets via UI or RESTful APIs.
  * Owners of a data source can add one or more targets (using pre-configured Systems.)
  * Supported targets are tables in TD and Aster, HDFS Sequence File and HBase table.
  * Support writing data in real-time, batch by records, and batch by time.
  * Guaranteed delivery; at-least once.
  * Built-in backpressure support for ingestion spikes and retention policies.
  * Pausing and resuming of writing to targets.
  * Monitor latency metrics of each source's target(s) over a day, hour, week or month.
* Administrator role capabilities via UI and RESTful APIs.
  * Security controls include LDAP integration for authentication and security.
  * Provide roles for administrator, user, and source owner.
  * OAUTH2 authentication for services.
  * Monitor and manage system targets and all user sources and associated targets.
  * Monitor and manage the platform and system services.
  * Generates email alerts for target error or service failures, if SMTP provided via API.

### Requirements

* Tested on the following data repositories:
  * Hadoop 2.3 - 2.6 (CDH 5.2+, HDP 2.3+)
  * Aster 6.10+
  * Teradata 15.10+
  * Hbase 1.1.2+
* Openstack (tested on version 2014.1.2 - Kilos)
* Signed, wildcard Security Certificate for subdomain
* DNS A - record
* LDAP configuration information
* SMTP internal relay (email notification)
* UI supported on evergreen web browsers
* More information - http://docs.uda.io/installation/prerequisites.html
* Licensing in Admin screen is disabled. Listener licensing will activate in a future update.
* Systems
  * Data streaming and writing available for the following systems:
    * Teradata (JDBC)
    * Aster (JDBC)
    * HDFS (Sequence file)
    * HBase (metadata & data as key/value).
  * Support for data streaming to 3rd party systems is coming soon.
  * Teradata and Aster tables must be created prior to using Listener.
  * No Kerberos for HDFS/Hadoop.
  * More information - http://docs.uda.io/user-guide/supported-systems.html
* Listener scaling or sizing must be defined at install time, for example VM definitions for both Openstack flavors and number of instances.
* Data duplication or loss might occur when a target writer is shut down. Listener will support at least once in an update.

### Errata and Known Bugs

* 1113 - Proper time is not returned in API responses.
* 1358 - Email alerts contain broken links.

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
