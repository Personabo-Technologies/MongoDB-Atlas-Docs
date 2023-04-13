Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Review Drop Index Recommendations

Share Feedback

On this page

  * Unused Indexes
  * Redundant Indexes
  * Hidden Indexes
  * Drop or Hide an Index

The Performance Advisor suggests dropping unused, redundant, and hidden
indexes to improve write performance and increase storage space.

## Tip

### See also:

To learn more about the impact of unnecessary indexes, see Remove Unnecessary
Indexes.

## Unused Indexes

An index is unused if it doesn't support any queries.

The Performance Advisor flags an index as unused if it hasn't supported a
query in 7 or more days after it was created or the server was restarted.

## Redundant Indexes

An index is redundant if another index supports any query that it could.

The Performance Advisor flags an index as redundant if it matches the prefix
of another index in the same collection.

## Example

If a collection contains the indexes:

  * `{ a: 1 }`

  * `{ b: -1 }`

  * `{ a: 1, b: -1 }`

`{ a: 1 }` is redundant because it matches the prefix `{ a: 1, b: -1 }`.

`{ b: -1 }` is not redundant because it does not match any prefix.

In the Performance Advisor, redundant indexes are marked with a red
`Redundant` badge. Below each redundant index, the Performance Advisor
displays the related indexes that cover it.

## Note

Related indexes are displayed for you to verify that the redundant index can
be dropped safely. Related indexes are not recommended for removal.

## Hidden Indexes

 _New in MongoDB version 4.4_

You can hide an index to evaluate the impact of dropping an index before you
drop it. Unhiding an index also takes less time than rebuilding a dropped
index. To hide and unhide an index by using the Atlas UI, see Create, View,
Drop, and Hide Indexes.

The Performance Advisor always recommends dropping hidden indexes. If you
determine that a hidden index is unnecessary, drop it.

## Note

Atlas doesn't use hidden indexes to support queries. They still impact write
performance and consume storage space. To learn more, see Hidden Indexes.

## Drop or Hide an Index

## Note

Consider hiding indexes before you drop them. Atlas supports hidden indexes
for MongoDB version 4.4 and higher.

To drop or hide an index by using the Performance Advisor:

1

### Navigate to the Performance Advisor Drop Indexes recommendations.

In the Performance Advisor tab, click View Recommendations on the Drop Indexes
card.

2

### On the index that you want to drop or hide, click Drop Index.

The Performance Advisor displays a dialog box with a link to the Atlas UI and
a copyable MongoDB Shell command to drop that index.

In MongoDB 4.4 and higher, the dialog box also provides a copyable MongoDB
Shell command to hide that index.

3

### Drop or hide the index by using the Atlas UI or MongoDB Shell.

To drop or hide an index by using the Atlas UI, click the Indexes tab, then
click the Drop Index or Hide Index icon next to the index. Atlas displays a
dialog box to confirm your selection. For more information, see Create, View,
Drop, and Hide Indexes.

To drop or hide an index by using the MongoDB Shell, paste and run the command
provided by the Performance Advisor.

← Review Index RankingEnable or Disable Performance Advisor for a Project →

