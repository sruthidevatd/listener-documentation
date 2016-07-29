Only users with administrative privileges will see **Manage Systems** and other **ADMIN** options in the navigation panel.

From **Manage Systems**, you can perform the following tasks:

- Search for a system by name
- Sort the list of systems in descending or ascending order
- Edit a system
- Create a system
- Delete a system

## Viewing the List of All Systems

1. In the ADMIN navigation panel, click **Manage Systems**.

Listener displays a lock icon next to the name of any system that is part of a production target.

## Searching for System by Name

1. In the **Search by system name** box, start typing any part of the system name. Listener automatically filters the list of systems as you type.
2. To clear this search filter and view all systems, delete the characters you typed in the **Search by system name** box.

## Sorting Systems in Descending or Ascending Order

By default, Listener sorts the systems in ascending order (A-Z).

1. Do one of the following:
 * To sort by descending order (Z-A), click the down arrow next to **NAME**.
 * To restore ascending order (A-Z), click the up arrow next to **NAME**.

## Editing a System

The **TEST CONNECTION** button appears after you enter all required information for the system.

1. In the card for the system you want to edit, click the pencil button.
2. Make the desired changes.
3. If required for this system, enter the **Username** and **Password**. 
4. Click **TEST CONNECTION**. A confirmation message appears indicating the status of the connection, either successful or failed.
5. Do one of the following:
 * If the connection failed, correct the settings, retest the connection, and click **SAVE**.
 * If the connection was successful, click **SAVE.**

## Creating a System

The **TEST CONNECTION** button appears after you enter all required information for the system.

1. In the lower right, click the orange floating action button.
2. In the **Name** box, enter a name for this system. For example: `Teradata EDW`
3. From the **System Type** list, select a type for this system. The type you select determines the parameters settings that appear.
4. Based on your system type, specify the following parameters: 
 * **Teradata**: System Host, System Port
 * **Aster**: System Host, System Port, Database
 * **HBase**: System Host, System Port, System Node, Zookeeper Host, Zookeeper Port, Zookeeper Parent Node
 * **HDFS**: HDFS Host, HDFS Port, and optionally HCatalog Details and credentials for HCatalog API configuration
5. If required for this system, enter the **Username** and **Password**.
6. Click **SAVE**. A confirmation message appears indicating the status of the connection, either successful or failed.
7. If the connection failed, correct the settings and click **SAVE**.

## Deleting a System

1. In the card for the system you want to delete, click the trash can button. A delete confirmation message appears.
2. Click **DELETE**.
