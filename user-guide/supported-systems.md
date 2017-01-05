Listener supports the following systems:

- Teradata 14.10 and later
- HDFS 2.3-2.6
- HBase 1.1.2
- Aster 6.10

Future releases of Listener will support additional systems. 

Listener supports the following message brokers for MQTT sources:

- ActiveMQ 5.14.0
- Mosquitto 1.3.4

The following properties are required to connect to and store data on the supported systems.

## Teradata

Listener requires the following properties to connect to Teradata:

* Host
* Port
* Username
* Password
* Database
* Table

Listener stores the host and port values. The Teradata target system stores the other values.

You must have permission to access and write to the target system and have the following privileges:

```
Select access on DBC.Tables[V][X]
Select access on DBC.Columns[V][X]
Select access on DBC.AllRights[V][X]
Select access on DBC.UDTInfo
```

For the `data` field, Teradata supports CLOB, JSON, or VARCHAR data type. If you use VARCHAR and send a message larger than the preallocated size of the column, it will be truncated.

Note: For Teradata version 14.10, you can send JSON messages as a VARCHAR or CLOB, but you cannot load data into a JSON column.

## HDFS

Listener requires the following properties to connect to HDFS:

* Host
* Port
* Username
* Password
* Data Path

HDFS systems optionally support HCatalog, which when configured, requires the following additional properties:

* HCatalog Host
* HCatalog Port
* HCatalog Database
* HCatalog Table
* HCatalog Username
* HCatalog Password

HDFS systems include the following default configurations that are not currently adjustable:

* File Rotation Size: 20MB
* File Rotation Time: 1 Day
* Block Size: 128MB
* Buffer Size: 4kb
* Replication Factor: 3
* File Naming Conventions: /user/defined/path/[target_id]/file.seq
* Compression Code: Sequence

You must have proper permission to create and modify files in the HDFS system for the defined data path.

## HBase

Listener requires the following properties to connect to HBase:

* Host
* Port
* Node
* Zookeeper Host
* Zookeeper Port
* Zookeeper Parent Node
* Table
* Column Family
* Username
* Password

You must have proper permission to access and write to the table and column family.

## Aster

Listener requires the following properties to connect to Aster:

* Host
* Port
* Username
* Password
* Database
* Table

You must have proper permission to access and write data to the database and table.
