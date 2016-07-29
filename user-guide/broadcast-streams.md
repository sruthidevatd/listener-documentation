Listener **Broadcast Streams** allow you to connect source data to external apps. The **Broadcast Streams** card is available in the source details view. From **Broadcast Streams**, you can perform the following tasks:

- Create streams
- Pause streams
- Restart streams
- Delete streams

## Accessing Broadcast Streams

1. From the **Dashboard** or **Data Sources**, click the source card. **Broadcast Streams** appears under **Source Info**.

## Creating a Broadcast Stream

3. In the **Broadcast Streams** card, click **NEW STREAM**.
3. In the **Enter stream name** box, enter a name for this stream and click **CREATE**. Listener generates a Websocket URL and Stream Secret Key, and displays messages confirming the stream has been saved and started.

You can create an unlimited number of streams for each source.

Users with administrative privileges can view, pause, restart, and delete **Broadcast Streams** from **Managed Targets**. For more information, see [Manage Targets](manage-targets.md). 

For information about using the Websocket URL and Stream Secret key for your external app, see [Targets](v1/targets.md).

## Pausing Broadcast Streams from Source Details

2. On the right side of the stream card, click the menu button and click **Pause  stream**. Listener pauses the stream, displays a confirmation message, and shows "(Paused)" next to the Websocket URL.

**Note:** If you see an error message when you try to pause a stream, that means Listener is still in the process of deploying the stream. Wait a few seconds and try again.

Users with administrative privileges can pause and restart streams from **Managed Targets**. For more information, see [Manage Targets](manage-targets.md). 


## Restarting Paused Broadcast Streams from Source Details

2. On the right side of the stream card, click the menu button and click **Start  stream**. Listener starts the stream and displays a confirmation message.

Users with administrative privileges can pause and restart streams from **Managed Targets**. For more information, see [Manage Targets](manage-targets.md). 

## Deleting a Broadcast Stream

1. On the right side of the stream card, click the menu button and click **Delete  stream**. Listener deletes the stream and displays a confirmation message.

Users with administrative privileges can delete streams from **Managed Targets**. For more information, see [Manage Targets](manage-targets.md). 