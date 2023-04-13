Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Deploy a Federated Database Instance

Share Feedback

On this page

  * Prerequisites
  * Procedure
  * Next Steps

 _Estimated completion time: 15 minutes_

This part of the tutorial will guide you through deploying a federated
database instance.

## Prerequisites

To complete this part of the tutorial, you will need to create a MongoDB Atlas
account, if you do not have one already.

## Procedure

1

### Log in to MongoDB Atlas.

2

### Select the Data Federation option on the left-hand navigation.

3

### Create a federated database instance.

  * For your first federated database instance, click Create a Federated Database.

  * For subsequent federated database instances, click Create Federated Database.

4

### Select the dataset for you federated database instance from the Data
Sources section.

Select AWS S3 from the dropdown and click Add Sample Data to use the MongoDB
hosted sample dataset.

5

### Drag and drop the following paths to the sample datasets from the Data
Sources pane on the left to the Federated Database Instance pane on the right.

  * `/airbnb/listingsAndReviews/{bedrooms string}/{review_scores.review_scores_rating int}/`

This path references the `airbnb` dataset, which contains the vacation home
listing details and customer reviews. To learn more about this dataset, see
Sample AirBnB Listings Dataset.

For this path, federated database instance utilizes partitions optimized for
queries on the `bedrooms` field and `review_scores.review_score_ratings`
fields.

  * `/analytics/accounts/{limit int}/`

This path references the `analytics` dataset, which contains data for a
typical finanacial services application. To learn more about this dataset, see
Sample Analytics Dataset.

For this path, federated database instance utilizes partitions optimized for
queries on the `limit` field.

  * `/analytics/customers/{birthdate isodate}/`

This data references the `analytics` dataset, which contains collections for a
typical finanacial services application. To learn more about this dataset, see
Sample Analytics Dataset.

For this path, federated database instance utilizes partitions optimized for
queries on the `birthdate` field.

  * `/analytics/transactions/{account_id int}/`

This path references the `analytics` dataset, which contains data for a
typical finanacial services application. To learn more about this dataset, see
Sample Analytics Dataset.

For this path, federated database instance utilizes partitions optimized for
queries on the `account_id` field.

  * `/mflix/movies/{type string}/{year int}/`

This path references the `mflix` dataset, which contains data on movies and
movie theaters. To learn more about this dataset, see Sample Mflix Dataset.

For this path, federated database instance utilizes partitions optimized for
queries on the `type` and `year` fields.

  * `/mflix/sessions.json`

This path references the `mflix` dataset, which contains data on movies and
movie theaters. To learn more about this dataset, see Sample Mflix Dataset.

This path does not contain any partition attributes and so, for queries
against data in the collection, Data Federation searches all the files in the
collection.

  * `/mflix/theaters/{theaterId string}/{location.address.zipcode string}/`

This path references the `mflix` dataset, which contains data on movies and
movie theaters. To learn more about this dataset, see Sample Mflix Dataset.

For this path, federated database instance utilizes partitions optimized for
queries on the `theaterId` and `location.address.zipcode` fields.

  * `/mflix/users.json`

This path references the `mflix` collection, which contains data on movies and
movie theaters. To learn more about this dataset, see Sample Mflix Dataset.

This path does not contain any partition attributes and so, for queries
against data in the collection, federated database instance searches all the
files in the collection.

  * `/nyc-yellow-cab-trips/{trip_start_isodate isodate}/{passenger_count int}/{fare_type string}/`

The path references the `nyc-yellow-cab-trips` dataset, which contains data on
the trips, including trip date, fare, and number of passengers.

For this path, federated database instance utilizes partitions optimized for
queries on the `trip_start_isodate`, `passenger_count`, and `fare_type`
fields.

6

### Optional: Change the name of the federated database instance from
FederatedDatabaseInstance0 to `GettingStarted` by clicking the associated
__icon.

You need not modify the database or collection name because the sample queries
that you run against the sample datasets later in this tutorial use the
default names.

7

### Click Save to create the federated database instance.

## Next Steps

Now that your federated database instance is deployed, proceed to Connect to
your federated database instance.

