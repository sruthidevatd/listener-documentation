Create targets from **Manage Sources** or the source details view.

1. Do one of the following:
 * From **Manage Sources** click the orange floating action button.
 * From the source details view, at the bottom of the **Targets** card, click **NEW TARGET**.

The **New Target** view appears.

## New Target

**New Target** settings are organized in the following three sections:
* **System Connection**
* **Target Options**
* **Target State**

**Note**: When you create a new target, you must first save settings in the **System Connection** section, next in the **Target Options** section, and then in the **Target State** section. Once you save settings, you can edit sections individually and in any order.

### Defining System Connection

1. In the **Target Name** box, enter a name for this target. For example: `Corporate Website Click Data`.
2. From the **Select the source** list, select a system type. The type of system you select determines the parameters settings that appear.
3. Based on your system type, specify the following parameters:
 * **Teradata**: Database, Table
 * **Aster**: Schema, Table
 * **HBase**: Column Family, Table
 * **HDFS**: HCatalog Table, HCatalog Username, HCatalog Password, Path, Serialization format
4. If required for this system, enter the **Username** and **Password**.
5. Click **SAVE**. A confirmation message appears indicating the status of the connection, either successful or failed.
6. If the connection failed, correct the settings and click **SAVE**.

### Specifying Target Options

1. Click **Target Options**.
2. Select one of the following batch options:
 * **Near Real-Time**: Writes to target after the source data travels from Listener ingest to streams
 * **by Records**: Writes to target every **100**, **1000**, **5000**, **10000**, or **20000** records
3. For a Teradata, Aster, or HBase system, select the **Target Column** for each of the following **Source Data** fields:
 * **Ingested Data**: Field with raw data sent to Ingest
 * **Source ID**: ID of the source to which packet was sent
 * **Timestamp**: Time the packet was ingested
 * **Batch ID**: Unique ID assigned to the packet upon arrival
4. Click **SAVE**.

**Note**: You can specify different batch options for records using the Listener API. For more information, see [Targets API](../api/v1/targets.md)

### Specifying Target State

1. Click **Target State**.
2. Select one of the following state options:
 * **Paused**: Target is paused and not writing data
 * **Writing**: Target is writing data
3. [Optional] To prevent anyone from editing or deleting this target, click  the **Lock Target** switch. The switch color changes from gray to blue, indicating the target is locked.
4. Click **SAVE**. A confirmation message appears indicating the target is saved, followed by the source details view with the updated target information.

### Target Table Examples

* [Aster](examples/aster.md)
* [Teradata](examples/teradata.md)
* [Streamer](examples/streamer.md)
