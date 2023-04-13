Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Read and Write with the Data API

Share Feedback

On this page

  * Overview
  * How the Data API Works
  * When to Use the Data API
  * Atlas App Services
  * Get Started
  * 1\. Enable the Data API
  * 2\. Create a Data API Key
  * 3\. Send a Data API Request
  * Configure the Data API
  * API Versions
  * Data Access Permissions
  * Authentication and API Keys
  * Deployment Models & Regions
  * Response Type
  * Call a Data API Endpoint
  * Specify the Request Data Format
  * Choose a Response Data Format
  * Authenticate Requests
  * Request Logs
  * Request Limitations
  * Request Traffic
  * Billing

## Overview

The MongoDB Atlas Data API is a managed service that lets you securely work
with data stored in Atlas using standard HTTPS requests. The Data API is not a
direct connection to your database. Instead, the API is a fully-managed
middleware service that sits between your cluster and the clients that send
requests.

You can use the Data API to connect to MongoDB Atlas from any platform that
supports HTTPS, including:

  * Web browsers

  * Web servers

  * CI/CD pipelines

  * Serverless & Edge compute environments

  * Mobile applications

  * Internet-Of-Things devices

You don't need to install any database drivers or opinionated libraries to
work with the Data API. Instead, you send standard HTTPS requests like the
following:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/data-abcde/endpoint/data/v1/action/insertOne' \  
      --header 'apiKey: TpqAKQgvhZE4r6AOzpVydJ9a3tB1BLMrgDzLlBLbihKNDzSJWTAHMVbsMoIOpnM6' \  
      --header 'Content-Type: application/json' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "learn-data-api",  
          "collection": "hello",  
          "document": {  
            "text": "Hello from the Data API!",  
          }  
      }'  
  
HIDE OUTPUT

    
    
    {"insertedId":"5f1a785e1536b6e6992fd588"}  
      
  
### How the Data API Works

Data API requests may resemble traditional database operations, like `find` or
`insertOne`, but the Data API is not a direct connection to your database.
Instead, the Data API adds additional authentication, authorization, and
correctness checks to ensure that your data is only accessed or modified in
the ways you allow. This allows you to safely access data in Atlas from
potentially vulnerable clients like web apps.

For each incoming request, the Data API:

  1.  **Authenticates the calling user.** This might involve validating an access token, logging in with header credentials, or directly assigning a specific runtime user based on your configuration.

  2.  **Authorizes the request.** This ensures that the user sent a well-formed request and has permission to perform the requested operation based on your endpoint authorization scheme.

  3.  **Runs the requested operation.** This might involve reading or writing data in Atlas with a generated endpoint or invoke a custom function that you wrote.

For requests that read or write data in Atlas, the Data API also enforces the
access control rules and document schemas defined in your App. This means that
users can only access data they're allowed to read and write. Requests fail if
they include an invalid write operation.

  4.  **Returns an HTTPS response to the caller.** The response includes the result of a generated endpoint operation or any data that you return from a custom endpoint. In the request, you can choose to receive the response in either JSON or EJSON format.

### When to Use the Data API

For server applications, and especially for high-load and latency sensitive
use-cases, we recommend connecting directly to Atlas with a MongoDB driver.
Operations called through a Data API endpoint take longer to complete than the
corresponding MongoDB operations called through a driver. Additionally, the
drivers provide more flexibility and control over how your operations are
executed. To learn more, visit the MongoDB Drivers documentation.

We recommend using the Data API when:

  * You want to run MongoDB operations from a web application or other client that you can't trust.

  * You can't or don't want to manage a MongoDB driver in your server-side environment. For example, the language you are using for your server does not have a driver.

  * Your server-side code runs in an edge compute environment that does not support database drivers or connection pooling.

  * You want to develop a new feature and prefer a flexible solution for working on the client side first before later creating and refining the API layer.

  * You want to integrate Atlas data access into a federated API gateway.

  * You want to connect to Atlas from an client not currently supported by a Realm SDK.

### Atlas App Services

The Data API is powered by Atlas App Services.

You can quickly set up and access the Data API through Atlas, which creates an
App Services App for you that's linked to the Atlas UI. The default
configuration and Atlas UI support API key authentication with several basic
permissions models.

You can define more complex API access permissions and customize your API with
your own endpoints by modifying the underlying App that was created for you or
enabling the API in your own App.

To learn more about App Services, how the Data API works, and how you can
customize it, see Data API in the App Services documentation.

## Get Started

Follow the steps below to set up the Data API and send your first requests.

### 1\. Enable the Data API

The Data API is disabled by default. To use the API, you need to turn it on in
the Atlas UI for one or more clusters.

Click Data API in the left navigation menu. On the following screen, select
one or more clusters that you want to enable the API on from the dropdown menu
and then click Enable the Data API.

## Note

You can enable or disable the Data API for a cluster at any time from the Data
API screen.

### 2\. Create a Data API Key

The Data API uses project-level API keys to manage access and prevent
unauthorized requests. Every request must include a valid Data API key.

A Data API key grants full read and write access every collection in a cluster
and can access any enabled cluster in the project.

## Important

Data API keys are not the same as the programmatic API keys used to access the
Atlas and App Services Administration APIs.

Click Create API Key, enter a unique name for the new key, and then click
Create API Key.

You can now see and copy your new API key for the first and only time. Once
you close the modal, Atlas will never expose the value again.

Copy the new API key and store it somewhere safe where you can reference it
later. Data API keys are sensitive, so make sure not to hardcode them directly
into user-facing apps or commit them to version control.

## Tip

You can delete a Data API key at any time. Any request that includes a deleted
key will fail. You might delete a key to prevent an existing client from
continuing to use the API or if you accidentally expose the key and need to
replace it.

### 3\. Send a Data API Request

You include your Data API key when you call action endpoints that read and
write documents in MongoDB. For a list of all available actions & endpoints,
see Data API Resources.

You can run the following commands in a shell to make sure everything works
and then start exploring:

## Tip

Make sure to replace placeholder values before you run each request:

  * `<Data API App ID>`: Your Data API App ID, which you can find in the URL Endpoint section of the UI.

  * `<Data API key>`: The Data API key you just created.

  * `<cluster name>`: The name of a cluster with the Data API enabled.

  1. Insert a test document:
    
        curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/json' \  
      --header 'apiKey: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "learn-data-api",  
          "collection": "people",  
          "document": {  
            "name": "John Sample",  
            "age": 42  
          }  
      }'  
  
  2. Then, find the test document that you just inserted:
    
        curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/findOne' \  
      --header 'Content-Type: application/json' \  
      --header 'apiKey: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "learn-data-api",  
          "collection": "people",  
          "filter": { "name": "John Sample" }  
      }'  
  
  3. Finally, delete the test document:
    
        curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/deleteOne' \  
      --header 'Content-Type: application/json' \  
      --header 'apiKey: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "learn-data-api",  
          "collection": "people",  
          "filter": { "name": "John Sample" }  
      }'  
  

## Configure the Data API

You can configure your API deployment and how users interact with the API.

### API Versions

The Data API uses a built-in versioning scheme to upgrade endpoints over time
while maintaining backwards compatibility. Incoming requests can specify which
version of an endpoint to use in the request URL and the Data API can serve
any version that you have enabled.

You must enable a new version before users can call endpoints with that
version. You can always enable the most recent Data API version. However, you
cannot enable an older version after a newer version has been released.

The following versions are currently supported:

  * `beta`

  * `v1`

### Data Access Permissions

The Atlas Data API allows you to define cluster-level read/write permissions
that apply to all incoming requests. You can define one of the following for
each cluster:

  *  **Read and Write** : Requests can read all data and can insert, modify, or delete data in any collection.

  *  **Read Only** : Requests can read all data in any collection but cannot write any data.

  *  **No Access** : Requests can't read or write any data in any collection.

For more complex permissions, you can define custom data access rules in the
managed Atlas Data API app.

### Authentication and API Keys

The Atlas Data API supports user authentication with API keys. Incoming
requests must include an API key in a request header. You can create up to 100
Data API keys.

To allow users to authenticate requests with another method, like a username
and password or a JSON web token, you can enable additional authentication
providers in the App Services App.

### Deployment Models & Regions

The App Services layer that runs the Data API processes requests on managed
servers hosted in deployment regions around the world. You can control where
you deploy your Data API and process requests using one of two deployment
models:

  *  **Global** deployment hosts your API on servers in every supported region across the world. The API automatically routes and processes incoming requests to the server that's nearest to the requesting user.

  *  **Local** deployment hosts your API servers in one specific deployment region in AWS or Azure. The API processes all incoming requests in the local region.

For a list of supported regions, see Deployment Models & Regions in the App
Services docs.

### Response Type

Endpoints can return data in one of two data formats, either JSON or EJSON.

By default, endpoints return JSON, which is a standard data format that is
widely supported modern langauges and platforms. However, JSON cannot
represent every data type that you can store in MongoDB and loses type
information for some data types.

You can also configure endpoints to return EJSON, which uses structured JSON
objects to fully represent the types that MongoDB supports. This preserves
type information in responses but requires that your application understands
how to parse and use EJSON.

## Tip

The official MongoDB drivers include methods for working with EJSON. You can
also download a standalone parser like bson on npm.

## Call a Data API Endpoint

You can call a Data API endpoint from any standard HTTP client. Each request
can include configuration headers and arguments in the request body.

### Specify the Request Data Format

Data API requests must include a `Content-Type` header to specify the data
format used in the request body.

  * Use `Content-Type: application/json` to represent standard JSON types in a Data API request body.

  * Use `Content-Type: application/ejson` to represent standard JSON types _and_ additional EJSON types in a Data API request body.

EJSON

JSON

    
    
    curl -X GET \  
      
      https://data.mongodb-api.com/app/<AppID>/endpoint/data/v1/action/insertOne \  
      -H 'apiKey: <API Key>' \  
      -H 'Content-Type: application/ejson' \  
      -H 'Accept: application/ejson' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "learn-data-api",  
          "collection": "hello",  
          "document": {  
            "_id": { "$oid": "629971c0d71aad65bd59c595" },  
            "greeting": "Hello, EJSON!",  
            "date": { "$date": { "$numberLong": "1654589430998" } }  
          }  
      }'  
  
HIDE OUTPUT

    
    
    { "insertedId": { "$oid": "629971c0d71aad65bd59c595" } }  
      
  
### Choose a Response Data Format

A request can include an `Accept` header to request a specific data format for
the response body, either JSON or EJSON. If a request does not include a valid
`Accept` header, the response uses the data format specified in your Data API
configuration.

EJSON

JSON

    
    
    curl -X GET \  
      
      https://data.mongodb-api.com/app/<AppID>/endpoint/data/v1/action/findOne \  
      -H 'apiKey: <API Key>' \  
      -H 'Content-Type: application/json' \  
      -H 'Accept: application/ejson' \  
      --data-raw '{  
         "dataSource": "Cluster0",  
         "database": "learn-data-api",  
         "collection": "hello",  
         "projection": { "greeting": 1, "date": 1 }  
      }'  
  
HIDE OUTPUT

    
    
    {  
      
      "_id": { "$oid": "629971c0d71aad65bd59c545"},  
      "greeting": "Hello, Leafie!",  
      "date": { "$date": { "$numberLong": "1654589430998" } }  
    }  
  
### Authenticate Requests

To keep your data secure and correct, generated Data API endpoints always run
in the context of a specific registered user.

Incoming requests must include request headers that authenticate a unique user
for the request. There are two ways to authenticate: Bearer authentication and
Credential authentication.

#### Bearer Authentication

Bearer authentication is the most secure authentication method for Data API
requests and is required for requests that originate from a web browser. This
method allows you to reuse an existing user session without storing their
login credentials.

Under this scheme, requests include a user access token in the `Authorization`
header. The access token is issued by App Services when a user authenticates
and is valid for a limited period of time. To learn more about how to get an
access token and use it to authenticate requests, see Authenticate Data API
Requests.

    
    
    curl -X POST 'https://data.mongodb-api.com/app/<AppID>/endpoint/data/v1/action/find' \  
      
       --header 'Authorization: Bearer <AccessToken>' \  
       --header 'Content-Type: application/json' \  
       --data-raw '{  
         "dataSource": "mongodb-atlas",  
         "database": "sample_mflix",  
         "collection": "movies",  
         "filter": {  
           "title": "The Matrix"  
         }  
       }'  
  
#### Credential Authentication

Credential authentication is useful while you're developing and in some
server-side environments. However, for most production use cases you should
prefer to use Bearer authentication.

Under this scheme, requests include plaintext user authentication information
from one of the following enabled authentication providers:

  * Email/Password

  * API Key

  * Custom JWT

Email/Password

API Key

Custom JWT

    
    
    curl -X POST \  
      
      https://data.mongodb-api.com/app/<AppID>/endpoint/data/v1/action/findOne \  
      -H 'email: <Email Address>' \  
      -H 'password: <Password>' \  
      -H 'Content-Type: application/json' \  
      --data-raw '{  
        "dataSource": "Cluster0",  
        "database": "learn-data-api",  
        "collection": "hello",  
      }'  
  
#### Authenticate Web Browser Requests

You can use the Data API from a web browser, but you must authenticate
requests using Bearer authentication with an access token instead of directly
including a user's API key or other credentials. Modern web browsers enforce
Cross-Origin Resource Sharing <Web/HTTP/CORS> (CORS), which blocks all Data
API requests that do not include a valid access token.

To learn how to get an access token and include it in a request, see
Authenticate Data API Requests.

## Request Logs

The Data API logs all requests and stores the logs for 30 days.

You can view them on the Data API screen in the Logs tab.

## Request Limitations

The Data API enforces the following limitations on all requests:

  * Incoming requests may not exceed 18 MB.

  * Response body content may not exceed 16 MB.

  * Request processing time may not exceed 90 seconds.

## Request Traffic

The Data API limits request traffic to 10,000 concurrent requests. Any
requests made beyond this limit return an HTTP response status code of 429 -
Too Many Requests. You can request a higher limit by filing a support ticket.

## Billing

The Data API has usage-based pricing measured by the underlying App Services
application. For details, see App Services Billing.

Data API usage is billed based on the following dimensions:

  *  **Requests:** Every action adds one request to your billed total regardless of whether or not the action is successful.

  *  **Compute:** Every action bills for time and memory that the server uses to process the action. The exact usage depends on your workload.

  *  **Data Transfer:** Every action bills for data returned to the caller in the response. The response may include the result set of the action or metadata that describes the result of the action.

← Custom Role ActionsData API Resources →

