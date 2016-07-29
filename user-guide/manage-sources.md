Only users with administrative privileges will see **Manage Sources** and other **ADMIN** options in the navigation panel.

From **Manage Sources**, you can perform the following tasks:

- View all, locked, or unlocked sources
- Search for a source by name
- Sort the list of sources in descending or ascending order
- Sort the list of sources by number of targets
- Edit a source
- Regenerate the API Key for a source
- Create a source
- Delete a source

**Note**: You can combine search and filter options.

## Viewing the List of All Sources

1. In the ADMIN navigation panel, click **Manage Sources**.

## Viewing All, Locked, or Unlocked Sources

1. Click one of the following tabs:
 * **ALL**: Lists all sources
 * **LOCKED**: Lists only locked sources
 * **UNLOCKED**: Lists only unlocked sources

## Searching for Source by Name

1. In the **Search by source name** box, start typing any part of the source name. Listener automatically filters the list of sources as you type.
2. To clear this search filter and view all sources, delete the characters you typed in the **Search by source name** box.

## Sorting Sources in Descending or Ascending Order

By default, the list of sources is sorted in ascending order (A-Z).

1. Do one of the following:
 * To sort by descending order (Z-A), click the down arrow next to **NAME**.
 * To restore ascending order (A-Z), click the up arrow next to **NAME**.

## Sorting Sources by Number of Targets

1. Do one of the following:
 * To sort by descending order (sources with most number of targets to least), click **TARGETS**.
 * To sort by ascending order (sources with least number of targets to most), click the up arrow next to **TARGETS**.

## Editing a Source

1. In the card for the source you want to edit, click the pencil button.
2. Make the desired changes and click **SAVE**.

**Note**: If you click **CANCEL** before saving, except in the case of regenerating the API key, the source information is not changed.

## Regenerating the API Key for a Source

**Notice**: When you regenerate an API key for a source, the previous API key will no longer work. You must provide the new API key to all data providers associated with this source. If you click **CANCEL** after regenerating the API key, this does *not* undo the key regeneration process. The new API key is now in effect.

1. In the card that lists the source for which you want a new API key, click the pencil button.
2. In the API box, click **REGENERATE**. A regenerate confirmation appears.
3. Click **REGENERATE**. The new API key appears in the **API Key** box.

## Creating a Source

Create sources from the **Data Sources** card, the **Dashboard**, or from **Manage Sources**. For more information, see [Create a Source](create-source.md)

### Deleting a Source

When a target is locked, the associated source and system are locked. You cannot delete a locked source.

**Notice**: When you delete a source, consumers of this source will no longer receive data with its API key.

1. In the card for the source you want to delete, click the trash can button. A delete confirmation message appears.
2. Click **DELETE**.
