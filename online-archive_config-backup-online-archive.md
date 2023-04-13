Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Back Up Online Archive Data

Share Feedback

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

After you archive data, it is not covered by the backup configuration on your
live Atlas cluster. However, archived data has the same redundancy guarantees
that the S3 vendor provides. If you have configured online archive on your
Atlas cluster, use Continuous Cloud Backups to mitigate data loss and have an
easy restore process.

Consider the following scenarios:

  * You archived part of your collection data and then backed up the remaining data on your Atlas cluster. If your cluster goes down when data exists in your cluster and in your Online Archive, you can restore your cluster data to the last state preserved in your backup strategy, and your Online Archive will remain unchanged.

  * You backed up data on your Atlas cluster and then archived part of your collection data. If your cluster goes down and you need to restore from a backup that is older than the time when archiving was stopped for the data, you may restore documents to your cluster that already exist in your Online Archive.

If you use Continuous Cloud Backups, you can replay the oplog to restore your
cluster to a point in time that matches the last time documents on the cluster
were archived and avoid any data loss or data redundancy.

If you have configured Continuous Cloud Backups and online archive on your
Atlas cluster, do the following to restore your cluster if your cluster goes
down:

  1. Pause online archive.

  2. Restore your cluster from the Continuous Cloud Backups.

  3. Resume online archive.

← Pause and Resume ArchivingRestore Archived Data →

