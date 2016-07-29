Only users with administrative privileges will see **Status** and other **ADMIN** options in the navigation panel.

**System Status** shows metrics for Listener microservices, including writers, services, and agents. Listener updates the metrics every 30 seconds.

From **System Status**, you can perform the following tasks:

- View summary and detailed metrics for Listener writers, services, and agents
- Restart a writer or Listener service

Listener provides the restart option in the event of a writer or service lockup, or if you need to force a configuration change.

## Accessing System Status

1. In the **ADMIN** navigation panel, click **Status**. 

## WRITERS

The **WRITERS** tab shows summary and detailed metrics for Listener writers.

1. From the **System Status** card collection, click **WRITERS**. 

### Writers Summary

**Writers Summary** shows the following metrics for all Listener writers:

- **Writers in Use**: Number of writers you created
- **Writer Slots Available**: Number of additional writers you can create
- **Writers Running**: Number of writers running
- **Writers Deploying**: Number of writers deploying
- **Writers Suspended**: Number of writers suspended (scaled down to zero instances)
- **Writers Unhealthy**: Number of writers that are unhealthy (no longer responding to health checks)

### Writer Services

**Writer Services** lists all Listener writer microservices. Each writer card includes an option to restart the service and the following metrics for each service:

- **mem (mb)**: Allocated memory
- **cpus**: Allocated CPUs
- **disk (mb)**: Allocated disk space
- **instances (#/#)**: Allocated/running instances

### Confirming Status of a Writer

1. In the writer service card, mouse over the icon next to writer name. Listener displays one of the following statuses:

 - running
 - unhealthy
 - deploying
 - suspended

### Restarting a Writer Service

1. From the far right column on the writer service card, click the restart button.

## LISTENER SERVICES

The **LISTENER SERVICES** tab shows summary and detailed metrics for Listener services.

1. From the **System Status** card collection, click **LISTENER SERVICES**. 

### Listener Services Summary

**Listener Services Summary** shows the following metrics for all Listener services:

- **Listener Services**: Total number of services
- **Services Running**: Number of running services
- **Services Deploying**: Number of deploying services
- **Writers Suspended**: Number of suspended services
- **Writers Unhealthy**: Number of unhealthy services

### System Services

**System Services** lists all Listener microservices. Each service card includes an option to restart the service and the following metrics for each service:

- **mem (mb)**: Allocated memory
- **cpus**: Allocated CPUs
- **disk (mb)**: Allocated disk space
- **instances (#/#)**: Allocated/running instances

### Confirming Status of a Service

1. In the service card, mouse over the icon next to the service name. Listener displays one of the following statuses:

 - running
 - unhealthy
 - deploying
 - suspended

### Restarting a Service

1. From the far right column on the service card, click the restart button.


## AGENT RESOURCES

The **AGENT RESOURCES** tab shows summary and detailed metrics for Listener agents.

1. From the **System Status** card collection, click **AGENT RESOURCES**. 

### Agents Resources Summary

**Agents Resources Summary** shows the following summary metrics for all agents:

- **Agents**: Total number of agents
- **CPU**: Percentage of allocated/used CPUs for all agents
- **Memory in GB**: Percentage of allocated/used memory for all agents
- **Disk in GB**: Percentage of allocated/used disk space for all agents

### Agents

**Agents** lists all Listener agent microservices. Each agent card includes the following metrics:

- **mem (mb)**: Allocated/used memory
- **CPU**: Allocated/used CPUs
- **disk (mb)**: Allocated/used disk space
- **writer slots available**: Number of writer slots available