# Administrator

Also ADMIN. User with permission to view and change all settings except __System Settings__.

# Data Source

Also Source. Source of streaming data and the primary component of Listener. For example, a website, mobile application, sensor, IoT, and so on.

# Ingest

Consumption of data streams.

# Latency

There are two latency measurements in Listener. Ingest-to-source latency is how long it takes Listener to receive data and sort it to the correct source. Target latency is how long it takes Listener to get data from the stream and write it to a target.

# Locked

Source or target that cannot be edited or deleted.

# Near Real-Time

Data is written to the target after the source data travels from Listener ingest to streams.

# Records

Metric that identifies the number of data packages sent from a source.

# Service

One of several microservices on which Listener is built. For example, installer, streamer, writer, log services, and so on.

# Size

Metric that identifies the physical size of a data package, in bytes.

# Source Secret Key

Unique code generated for each source and required by Listener to stream data, considered private information and should not be shared.

# Starred

Source selected as a favorite so it appears in the Listener **Dashboard**.

# Status

Status of each Listener microservice.

# Super User

System-level user with permission to change LDAP settings and system password.

# System

Teradata, Aster, or Hadoop system on which the target resides.

# System Settings

LDAP credentials and **Super User** password.

# Target

Database, table, or file to which data is written.

# User

Anyone who is a valid member of the LDAP group configured in **System Settings**.

# Volume Size

Size of a source compared to all other sources (**Small**, **Medium**, or **Large**). Allocates infrastructure resources. Can be changed at anytime.

# Writer

Service that writes data to the target.
