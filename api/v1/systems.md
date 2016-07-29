Systems are records that reference available data systems to which you want to write data. Only Administrators can modify system records.

* [System Object](#system-object)
* [System Types](#system-types)
* [Get a List of Systems](#get-a-list-of-systems)
* [Get a System](#get-a-system)
* [Create a System](#create-a-system)
* [Update a System](#update-a-system)
* [Delete a System](#delete-a-system)
* [Validate a System](#validate-a-system)

## System Object

A system includes the following properties:

Property    | Type    | Example | Description
------------|---------|---------|-------------
system_id   | string  | `9dda5570-70e0-45be-8449-83f33320cd08` | ID of the system.
owner       | array   | `["jd123456"]` | Array of users IDs with owner permissions.
created_at  | string  | `2015-07-04T10:20:00Z` | Timestamp of moment of creation.
created_by  | string  | `av012345` | ID of user that created the system.
updated_at  | string  | `2015-12-25T10:20:00Z` | Timestamp when last updated.
updated_by  | string  | `jd123456` | ID of user that last updated the system.
name        | string  | `My Data System` | Name of the system.
description | string  | `A superb data system` | Description of the system.
system_type | string  | `teradata` | Type of system.
system_info | object  | `{ "login": "ip112233", "port": "8080" }` | Connection information object. Contents may vary by system type.
state       | string  | `1` | State of the system, enabled or disabled.
properties  | object  | `{"hcatalog_url": "example.com"}` | Additional properties that might be used by this system type.

The properties *system_id*, *created_at*, *created_by*, *updated_at*, and *updated_by* are assigned by the Teradata Listener API at the moment of creation and are __Read-Only__.

The properties *owner* and *state* are assigned by the Teradata Listener API at the moment of creation if not declared.

The properties *system_id*, *created_at*, *created_by*, *updated_at*, *updated_by* and *secret* are assigned by the Teradata Listener API at the moment of creation and are __Read-Only__.

The property *state* can be changed only by deleting an item.

## System Types

Listener supports four types of target systems. These targets have slightly different configuration options.

* [Teradata](#teradata)
* [Aster](#aster)
* [HDFS](#hdfs)
* [HBase](#hbase)

#### Teradata

A Teradata target requires a `host` and `port`.

```json
{
  "system_type": "teradata",
  "system_info": {
    "host": "my.teradata.host",
    "port": "1025"
  }
}
```

#### Aster

An Aster target requires a `database`, `host`, and `port`.

```json
{
  "system_type": "aster",
  "system_info": {
    "database": "mydatabase",
    "host": "my.aster.host",
    "port": "2406"
  }
}
```

#### HDFS

An HDFS target requires `host` and `port` properties, which should contain a full HDFS connection string. It also requires a `properties` object with the `webhcat` values.

```json
{
  "system_type": "hdfs",
  "system_info": {
    "host": "myhdfs.host",
    "port": "2181"
  },
  "properties": {
    "webhcat": {
      "host": "host",
      "port": "port",
      "database": "db",
      "username": "user",
      "password": "pass"
    }
  }
}
```

#### HBase

A HBase system requires `host` , `node`, and `port` in the `system_info` property. It also requires the values in `properties` for `zookeeper_host`, `zookeeper_port`, and `zookeeper_parent`.

```json
{
  "system_type": "hbase",
  "system_info": {
    "host": "myhbase.host",
    "node": "/hbase-node",
    "port": "2181"
  },
  "properties": {
    "zookeeper_host": "zookeeper.host",
    "zookeeper_port": "3000",
    "zookeeper_parent": "/parent-node"
  }
}
```

## Get a List of Systems

Load a list of all systems in Listener.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/systems HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/systems
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "system_id": "9dda5570-70e0-45be-8449-83f33320cd08",
    "owner": ["jd123456"],
    "name": "My System",
    "description": "A superb system",
    "system_type": "hadoop",
    "system_info": { "login": "ip112233", "port": "8080" },
    "state": "1"
  },
  ...
]
```

#### Response Codes

Code | Meaning
---- | -------
201  | Systems were returned successfully.
401  | 401_STATUS

## Get a System

Get a single system by a given system id.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/systems/{system_id} HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/systems/9dda5570-70e0-45be-8449-83f33320cd08
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "system_id": "9dda5570-70e0-45be-8449-83f33320cd08",
  "owner": ["jd123456"],
  "name": "My System",
  "description": "A superb system",
  "system_type": "hadoop",
  "system_info": { "login": "ip112233", "port": "8080" },
  "state": "1"
}
```

#### Response Codes

Code | Meaning
---- | -------
201  | System was returned successfully.
401  | 401_STATUS
404  | 404_STATUS

## Create a System

To create a new system, provide a JSON object of the properties for the new system. If read-only properties are supplied, they will be ignored.

#### Definition

```http
POST https://listener-app-services.teradata.com/v1/systems HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X POST \
  -d '{
    "name": "My System",
    "description": "A superb system",
    "system_type": "hadoop",
    "system_info": { "login": "ip112233", "port": "8080" }
  }' \
  -i \
  https://listener-app-services.teradata.com/v1/systems
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "system_id": "9dda5570-70e0-45be-8449-83f33320cd08",
  "owner": ["jd123456"],
  "name": "My System",
  "description": "A superb system",
  "system_type": "hadoop",
  "system_info": { "login": "ip112233", "port": "8080" },
  "state": "1"
}
```

#### Response Codes

Code | Meaning
---- | -------
201  | System was created successfully.
400  | 400_STATUS
401  | 401_STATUS


## Update a System

To update a system, send a JSON object with updated values for one or more of the __writable__ system properties.  If read-only fields are supplied, they will be ignored. All property values from the previous version of this system are carried over by default, if not included in the hash.

#### Definition

```http
PATCH https://listener-app-services.teradata.com/v1/systems/{system_id} HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PATCH \
  -d '{
    "system_id": "9dda5570-70e0-45be-8449-83f33320cd08",
    "owner": ["jd123456"],
    "name": "My Updated System",
    "description": "A superb system",
    "system_type": "hadoop",
    "system_info": { "login": "ip112233", "port": "8080" },
    "state": "1"
  }' \
  -i \
  https://listener-app-services.teradata.com/v1/systems/9dda5570-70e0-45be-8449-83f33320cd08
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
  "system_id": "9dda5570-70e0-45be-8449-83f33320cd08",
  "owner": ["jd123456"],
  "name": "My Updated System",
  "description": "A superb system",
  "system_type": "hadoop",
  "system_info": { "login": "ip112233", "port": "8080" },
  "state": "1"
}
```

#### Response Codes

Code | Meaning
---- | -------
201  | System was updated successfully.
400  | 400_STATUS
401  | 401_STATUS
404  | 404_STATUS

## Delete a System

Deleting a system will set the state to `0` to disable it. Once a system is disabled, it will not appear for users.

#### Definition

```http
DELETE https://listener-app-services.teradata.com/v1/systems/{system_id} HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X DELETE \
  -i \
  https://listener-app-services.teradata.com/v1/systems/9dda5570-70e0-45be-8449-83f33320cd08
```

#### Example Response

```http
HTTP/1.1 204 No Content
```

#### Response Codes

Code | Meaning
---- | -------
204  | System was deleted successfully.
400  | 400_STATUS
401  | 401_STATUS
404  | 404_STATUS

## Validate a System

You can validate a system's connection settings before trying to save it. The format of the body contains only the connection details and does not match the normal system object.

#### Definition

```http
POST https://listener-app-services.teradata.com/v1/systems/validate HTTP/1.1
```

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X POST \
  -d '{
    "system_type": "hbase",
    "host": "myhbase.host",
    "port": "2181",
    "node": "/mynode",
    "username": "username",
    "password": "password"
  }' \
  -i \
  https://listener-app-services.teradata.com/v1/systems/validate
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

#### Response Codes

Code | Meaning
---- | -------
200  | System is valid.
400  | 400_STATUS
401  | 401_STATUS
404  | 404_STATUS
