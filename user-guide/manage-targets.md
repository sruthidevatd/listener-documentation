Only users with administrative privileges will see **Manage Targets** and other **ADMIN** options in the navigation panel.

From **Manage Targets**, you can perform the following tasks:

- View all, locked, or unlocked targets
- Search for a target by name
- Filter the list of targets by system
- Filter the list of targets by source
- Sort the list of targets in descending or ascending order
- Sort the list of targets by date and time created or updated
- Edit a target
- Edit a Broadcast Stream
- Create a target
- Delete a target

**Note**: You can combine view, filter, and search options.

**Note**: The list of targets includes any Broadcast Streams you created. From **Manage Targets**, you can edit or delete Broadcast Streams. For more information about creating Broadcast Streams, see [Broadcast Streams](broadcast-streams.md).

## Viewing the List of Targets

1. In the ADMIN navigation panel, click **Manage Targets**. Listener displays a list of targets, including the date each target was created and updated.

## Viewing All, Locked, or Unlocked Targets

1. Click one of the following tabs:
 * **ALL**: Lists all targets
 * **LOCKED**: Lists only locked targets
 * **UNLOCKED**: Lists only unlocked targets

 Listener displays a list of targets on individual cards that show the target name, path, and one of the following statuses:
 * **Target is deploying**: Write process is starting.
 * **Target is pausing**: Target is in process of being paused.
 * **Target is paused**: Target is paused.
 * **Target is writing data in...**: Target is writing data in time batches, record batches, or near real-time. For Broadcast Streams, near real-time is the only writing status that applies.

## Filtering Targets by System

1. From the **Filter System** list, click the system type by which you want to filter targets.
2. To clear this filter, click the delete button next to the system type.

## Filtering Targets by Source

1. From the **Filter Source** list, click the source name by which you want to filter targets.
2. To clear this filter, click the delete button next to the source name.

## Searching for Target by Name

1. In the **Search by target name** box, start typing any part of the target name. Listener automatically filters the list of targets as you type.
2. To clear this search filter, delete the characters you typed in the **Search by target name** box.

## Sorting Targets in Descending or Ascending Order

By default, Listener sorts targets by name in ascending order (A-Z).

1. Do one of the following:
 * To sort by descending order (Z-A), click the down arrow next to **NAME**.
 * To restore ascending order (A-Z), click the up arrow next to **NAME**.

## Sorting Targets by Date and Time Created or Updated

By default, Listener sorts targets by name in ascending order (A-Z).

1. Do one of the following:
 * To sort by date and time the targets were created, click **CREATED**.
 * To sort by date and time the targets were updated, click **UPDATED**.

## Editing a Target

1. In the card that lists the target you want to edit, click the pencil button.
2. Under **Target State**, check **Locked status**. If the **Lock Target** switch is blue, the target is locked and you cannot edit the target. To unlock a target, do the following:
 1. Next to **Target State**, click the pencil button.
 2. Click the **Lock Target** switch. The switch color changes from blue to gray, which means the target is unlocked.
 3. Click **SAVE**.
4. Next to **System Connection** or **Target Options**, click the pencil button, make the desired changes, and click **SAVE**.
5. Next to **Target State**, click the pencil button, make the desired changes to target writing status and locked status, and click **SAVE**.

## Editing a Broadcast Stream

1. In the card that lists the stream you want to edit, click the pencil button.
2. Next to **Target State**, click the pencil button, make the desired changes to target writing status and locked status, and click **SAVE**.

## Creating a Target

Create targets from **Manage Targets** or the source details view. For more information, see [Create a Target](create-target.md).

## Deleting a Target

This procedure applies to all targets, including Broadcast Streams.

**Note**: You cannot delete a locked target. To unlock a target, see [Editing a Target](#editing-a-target).

1. Do one of the following to delete an unlocked target:
 * In the **Manage Targets** view, click the trash can button.
 * In the **Edit Target** view, click **DELETE TARGET**. A delete confirmation message appears.
2. Click **DELETE**.
