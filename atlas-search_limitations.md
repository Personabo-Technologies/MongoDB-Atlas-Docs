Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search M0 (Free Cluster), M2, and M5 Limitations

Share Feedback

The following limitations apply to Atlas Search on `M0`, `M2`, and `M5`
clusters only:

  * You cannot create more than:

    * 3 indexes on `M0` clusters.

    * 5 indexes on `M2` clusters.

    * 10 indexes on `M5` clusters.

There are no limits to the number of indexes you can create on `M10+`
clusters.

  * When you reach the maximum number of indexes allowed for the cluster tier, you can upgrade your cluster tier to create additional indexes. If you upgrade your cluster tier, the indexes are rebuilt on the new cluster tier, which triggers an initial sync.

  * An index definition JSON object cannot exceed 3KB in size.

  * Index builds with more than 300 fields fail.

  * Lucene's default clause limit of 1024 applies to any `BooleanQuery` created for searches.

  * The synonyms collection can't exceed 10,000 documents.

← Review Atlas Search MetricsFAQ: Atlas Search →

