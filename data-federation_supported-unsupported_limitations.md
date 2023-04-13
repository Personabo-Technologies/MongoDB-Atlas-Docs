Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data Federation Limitations

Share Feedback

Data Federation does not support the following features:

  * Creating Indexes

  * Authenticating with methods other than SCRAM or X.509 Certificates

  * Monitoring federated database instances with Atlas monitoring tools

  * Creating a federated database instance with S3 buckets from more than one AWS account

  * Querying documents larger than 16MB

  * Returning documents in the same order across queries unless imposed by the query operators used

  * Having more than 60 _guaranteed_ simultaneous connections per region to a federated database instance

  * Running more than 30 simultaneous queries on your federated database instance

If your aggregation pipeline only contains the $currentOp stage, Atlas Data
Federation doesn't enforce the limit on the maximum number of simultaneous
queries. You can run queries that only contain the $currentOp stage even after
you reach the maximum number of simultaneous queries.

## Important

Atlas Data Federation automatically expires your cursor if you do not consume
at least 16MiB of results every 1 minute.

← `$sql`What is MongoDB Atlas Search? →

