Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Navigate to the Atlas Search page for your project.

Share Feedback

  1. If it isn't already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it isn't already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

# Create an index.

Share Feedback

  * For your first index, click Create Search Index.

  * For subsequent indexes, click Create Index.

3

# Select a Configuration Method and click Next.

Share Feedback

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

# Enter the Index Name, and set the Database and Collection.

Share Feedback

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_training` database, and select the collection.

    * To create an index for the `companies` collection, select `companies`.

    * To create an index for the `inspections` collection, select `inspections`.

5

# Specify an index definition.

Share Feedback

The following index definition dynamically indexes the fields of supported
types in the collection. You can use the Visual Editor or the JSON Editor in
the Atlas user interface to create the index.

Visual Editor

JSON Editor

  1. Click Next.

  2. Review the `"default"` index definition for the collection.

6

# Click Create Search Index.

Share Feedback

7

# Close the You're All Set! Modal Window.

Share Feedback

A modal window displays to let you know your index is building. Click the
Close button.

8

# Wait for the index to finish building.

Share Feedback

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

What is MongoDB Atlas? →

