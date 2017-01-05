Elastic Search data is backed up on the first three mesos-masters servers every day at 3:30 a.m. You can change the time of backup by modifying the job for consule-backup using Cron.

### Backup
To execute an on-demand backup: `# /usr/local/bin/consulate-backup`

**Note**: Backups are created in: `/opt/listener/backup/consul-$HOSTNAME-$DATE.gz`

### Restore
To restore from a consul backup: `# /usr/local/bin/consulate-restore consulbackup-$HOSTNAME-$DATE.gz`

**Note**: The consul backup must be gziped and located in: `/opt/listener/backup/` 
