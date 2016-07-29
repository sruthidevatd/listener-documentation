# Backups
Teradata Listener allows you to backup and restore configuration data. This data can be migrated from one environment to another to replicate existing configurations, or restore an environment to a previous state. Listener is comprised of 2 data stores, consul and elastic search. Each service has a unique way to backup and restore. Backed up data stays on the systems for 14 days, after which time it is removed.

**When restoring a previous backup, consul and elastic search must be restored at the same time.**
