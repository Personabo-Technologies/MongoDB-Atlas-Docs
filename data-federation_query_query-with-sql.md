Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Query with SQL

Share Feedback

## Note

### Preview

The support for SQL queries is available as a Preview feature. This feature
and the corresponding documentation may change at any time during the Preview
phase.

You can query your federated database instance using Atlas SQL. This
capability allows you to create SQL queries to visualize, graph, and report on
your Atlas data using relational business intelligence tools such as Tableau.

## Note

Atlas SQL only supports reading through Atlas Data Federation.

The SQL interface is available by default when you create a federated database
instance. Atlas Data Federation automatically creates collection schemas for
SQL query compilation and type inference. To learn more about the schema, see
Schema Management.

To run queries using the SQL interface, connect using the MongoDB JDBC Driver
or one of the BI tool Named Connectors. To learn more about the different
connect options, see Connect.

## Components

The SQL interface includes the following components:

### Federated Database Instance

A federated database instance is a deployment of Atlas Data Federation. Each
federated database instance contains virtual databases and collections that
map to data in your data stores. This also provides a SQL schema and
translates SQL queries between your BI tool and your Atlas data.

### JDBC Driver or Named Connector

The JDBC Driver or a Named Connector provides a standard method to connect to
a BI tool. Depending on what your BI tool supports, you can use JDBC or a
specific Named Connector.

### BI Tool

A visualization and reporting tool, such as Tableau.

← Manage Atlas Data Federation Query LimitsGet Started →

