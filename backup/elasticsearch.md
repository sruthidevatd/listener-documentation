## Elastic Search
Elastic Search data is backed up on the first three mesos-slave servers everyday at 3:30 a.m. You can change the time of backup by modifying the job for elastic-dump using Cron.

### Backup
To execute an on-demand backup:
```
# /usr/local/bin/elasticdump
```

The data backup file is created as: `/opt/listener/backup/elasticsearch-$HOSTNAME-$DATE.json.gz`
The mapping backup file is created as: `/opt/listener/backup/elasticsearch-mapping-$HOSTNAME-$DATE.json.gz`

### Restore
Restoring from a restore point will overwrite existing Listener data. Currently, incremental backups are not supported.

To restore from a restore point: 

```
# /usr/local/bin/elasticrestore elasticsearch-$HOSTNAME-$DATE.json.gz elasticsearch-mapping-$HOSTNAME-$DATE.json.gz
```
**Note**: The file must be gziped and located in: `/opt/listener/backup/`
