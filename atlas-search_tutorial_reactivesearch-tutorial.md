Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Build a Search UI with Atlas App Services

Share Feedback

On this page

  * Prerequisites
  * Deploy the Reactive Search API
  * Host a Search UI
  * Run Atlas Search Queries

This tutorial describes how to set up Atlas Search and use Atlas App Services
to build a search UI with Searchbox and ReactiveSearch UI libraries. It also
demonstrates how to run Atlas Search queries using the ReactiveSearch App
Services function endpoint.

This tutorial takes you through the following steps:

  1. Deploy the ReactiveSearch API as an App Services function.

  2. Host a search UI with App Services's hosting.

  3. Run Atlas Search queries.

## Prerequisites

Before you begin:

  * Ensure that your Atlas cluster meets the requirements described in the Prerequisites.

  * Create an Atlas Search index named `default` that uses dynamic mappings against the `sample_airbnb.listingsAndReviews` collection from the sample datasets. To learn more, see Create an Atlas Search Index.

## Deploy the Reactive Search API

In this section, you will deploy the ReactiveSearch API as an App Services
function.

1

### Create API keys for your Atlas organization or project and configure the
API access list.

## Note

You need the public and private API key values to deploy the Reactive Search
API.

To create the API keys and configure the API access list for the API keys, see
the following pages:

  * Create an API Key in an Organization

For an organization, you must assign the API key the `Organization Member`
organization role or higher and invite the organization API key to your
project.

  * Create an API Key for a Project

For a project, you must assign the API key the `Project Owner` project role.

2

### (Optional) Set the following environment variables for you API key.

## Note

If you don't set the following variables, you must manually specify your API
keys when you deploy the ReactiveSearch API.

  1. Replace `private_key_value` with your private API key and run the following command:
    
        private_key={private_key_value}  
      
  
  2. Replace `public_key_value` with your public API key and run the following command:
    
        public_key={public_key_value}  
      
  

3

### Create an App Services app and copy its ID.

  1. Go to App Services.

  2. Create an app.

  3. Find Your App ID.

  4. Copy the App ID from the application dashboard.

4

### (Optional) Set the environment variable for your App Services app.

## Note

If you don't set the following variable, you must manually specify your App ID
when you deploy the ReactiveSearch API.

Replace `app_id_value` with your App Services App ID and run the following
command:

    
    
    app_id={app_id_value}  
      
  
5

### Clone the `reactivesearch-realm-project` repository.

Run the following command to clone the reactivesearch-realm-project
repository:

    
    
    git clone https://github.com/appbaseio/reactivesearch-realm-function.git  
      
  
6

### Install dependencies.

  1. Change the working directory:
    
        cd reactivesearch-realm-function  
      
  
  2. Run one of the following commands to install the project dependencies:
    
        yarn  
      
      
        npm install  
      
  

7

### Deploy the ReactiveSearch API.

## Note

If you didn't set the environment variables, you must manually specify your
API keys and App ID when you deploy the ReactiveSearch API.

  1. Run one of the following commands:

    * To deploy the ReactiveSearch API without basic authentication enabled, run the following command:
        
                node rs-cli --private-api-key $private_key --api-key $public_key --app-id $app_id  
          
  
    * To deploy the Reactive Search API with basic authentication enabled replace `my-user` and `my-password` with your username and password, and run the following command:
        
                node rs-cli --private-api-key $private_key --api-key &$public_key --app-id $app_id --app-authentication <my-user>:<my-password>  
          
  
If the deploy succeeds, the output should resemble the following example:

    
        1|  Successfully deployed webhook.  
    |  
    2|   
      
    3|  Deployed webhook endpoint : https://us-east-1.aws.webhooks.mongodb-realm.com/api/client/v2.0/app/application-0-tzwlw/service/http_endpoint/incoming_webhook/reactivesearch  
    4|   
      
    5|  You can make a test request to this webhook using this curl command  
    6|   
      
    7| curl -XPOST https://us-east-1.aws.webhooks.mongodb-realm.com/api/client/v2.0/app/application-0-tzwlw/service/http_endpoint/incoming_webhook/reactivesearch  \  
    8|         -H "Content-Type: application/json" \  
    9|         -d '{  
    10|              "query": [{  
    11|                           "id": "search",  
    12|                           "dataField": "*",  
    13|                           "size": 5  
    14|              }],  
    15|              "mongodb": {  
    16|                           "db": "'"$database"'",  
    17|                           "collection": "'"$collection"'"  
    18|              }  
    19| }'  
  
  2. Copy the webhook URL (highlighted in the previous example) from your output.

  3. (Optional) Copy the curl command from your output, specify a database and collection (highlighted in the following example), and run the command to verify the webhook:
    
        1| curl -XPOST https://us-east-1.aws.webhooks.mongodb-realm.com/api/client/v2.0/app/application-0-tzwlw/service/http_endpoint/incoming_webhook/reactivesearch  \  
    |  
    2|         -H "Content-Type: application/json" \  
    3|         -d '{  
    4|              "query": [{  
    5|                           "id": "search",  
    6|                           "dataField": "*",  
    7|                           "size": 5  
    8|              }],  
    9|              "mongodb": {  
    10|                           "db": "'"sample_airbnb"'",  
    11|                           "collection": "'"listingsAndReviews"'"  
    12|              }  
    13| }'  
  

## Host a Search UI

In this section, you will host a search UI with hosting from App Services. The
ReactiveSearch App Services function endpoint exposes a REST API that all of
the ReactiveSearch and Searchbox UI libraries use to express the declarative
search intent.

## Note

This tutorial uses the sample queries in `facet-filters` example. The `by-
usecases` directory contains several other examples. Repeat the following
steps for any other use cases that you want to try.

1

### Enable hosting from the App Services UI.

  1. Log in to App Services.

  2. Click Hosting in the left navigation pane.

  3. Click Enable Hosting and complete the steps to enable hosting. To learn more, see Enable Hosting.

2

### Download the search UI files.

  1. Open a terminal and run the following command to clone the searchbox repository:
    
        git clone https://github.com/appbaseio/searchbox.git  
      
  
  2. Run the following command to make a temporary directory.
    
        mkdir tmp  
      
  
  3. Copy the local search UI directory to the temporary directory:
    
        cp -R searchbox/packages/react-searchbox/examples/by-usecases/facet-filters tmp  
      
  

3

### Edit the `App.js` file.

  1. Open the `App.js` file from the following directory:

`/tmp/facet-filters/src`

  2. Replace the URL on line 11 with your webhook URL and save the file.

4

### Build the search UI.

  1. Run the following command to change the working directory:
    
        cd ../  
      
  
  2. Run one of the following commands to build the search UI application:
    
        yarn && yarn build  
      
      
        npm install && npm run build  
      
  
The command places the search UI files in the `/tmp/facet-filters/build`
directory.

5

### Upload the search UI files from the `build` directory.

  1. Log in to App Services.

  2. Click Hosting in the left navigation pane.

  3. Drag and drop the search UI files from your local `build` directory including the `static` folder and subfolders onto the Hosting page.

## Note

The new `index.html` file replaces the existing one.

  4. Click Review Draft and Deploy.

This action generates a public URL for your search UI application.

## Run Atlas Search Queries

You can now access the hosted URL and run Atlas Search queries using the
ReactiveSearch App Services function endpoint.

1

### Access the hosted URL.

  1. Click Hosting in the left navigation pane.

  2. Select the Files tab.

2

### Copy the hosted URL.

The URL appears at the top of the Files pane in the following format:

    
    
    {app-id}.mongodbstitch.com  
      
  
3

### Open the hosted page.

Paste the URL into your browser.

4

### View Atlas Search query results.

View the search query results for the `facet-filter` use case in the Searchbox
UI.

← How to Run `$unionWith` with an Atlas Search `$search` QueryHow to Check for
Null and Non-Null Values with Atlas Search →

