Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Sample Analytics Dataset

Share Feedback

On this page

  * Collections
  * `sample_analytics.accounts`
  * `sample_analytics.customers`
  * `sample_analytics.transactions`

The `sample_analytics` database contains three collections for a typical
finanacial services application. It has customers, accounts, and transactions.
These are used as part of the exercises for the MongoDB Training on Data
Analysis.

To learn how to load the sample data provided by Atlas into your cluster, see
Load Sample Data.

## Collections

The `sample_analytics` database contains the following collections:

Collection Name

|

Description  
  
|  
  
accounts

|

Contains details on customer accounts.  
  
customers

|

Contains details on customers.  
  
transactions

|

Contains customer transactions.  
  
### `sample_analytics.accounts`

This collection contains account details for users. Each document contains an
account id, a limit and the products that a customer has purchased.

#### Indexes

The `sample_analytics.accounts` collection contains the following indexes:

Name

|

Index

|

Description  
  
||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.  
  
#### Sample Document

    
    
    {  
      
      "account_id": 470650,  
      "limit": 10000,  
      "products": [  
        "CurrencyService",  
        "Commodity",  
        "InvestmentStock"  
      ]  
    }  
  
### `sample_analytics.customers`

This collection contains customers details including what accounts they hold
users. Each document contains username, name, address, birth date, email
address, a list of the accounts held, and details on the tier(s) and related
benefits they are entitled to.

#### Indexes

The `sample_analytics.customers` collection contains the following indexes:

Name

|

Index

|

Description  
  
||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.  
  
#### Sample Document

    
    
    {  
      
     "username": "lejoshua",  
     "name": "Michael Johnson",  
     "address": "15989 Edward Inlet\nLake Maryton, NC 39545",  
     "birthdate": {"$date": 54439275000},  
     "email": "courtneypaul@gmail.com",  
     "accounts": [  
       470650,  
       443178  
     ],  
     "tier_and_details": {  
       "b5f19cb532fa436a9be2cf1d7d1cac8a": {  
          "tier": "Silver",  
          "benefits": [  
            "dedicated account representative"  
          ],  
          "active": true,  
          "id": "b5f19cb532fa436a9be2cf1d7d1cac8a"  
          }  
     }  
    }  
  
### `sample_analytics.transactions`

This collection contains transactions details for users. Each document
contains an account id, a count of how many transactions are in this set, the
start and end dates for transactions covered by this document, and a list of
sub documents. Each sub document represents a single transaction and the
related information for that transaction.

#### Indexes

The `sample_analytics.transactions` collection contains the following indexes:

Name

|

Index

|

Description  
  
||  
  
`_id_`

|

`{ "_id": 1 }`

|

Primary key index on the `_id` field.  
  
#### Sample Document

    
    
    {  
      
      "account_id": 794875,  
      "transaction_count": 6,  
      "bucket_start_date": {"$date": 693792000000},  
      "bucket_end_date": {"$date": 1473120000000},  
      "transactions": [  
        {  
          "date": {"$date": 1325030400000},  
          "amount": 1197,  
          "transaction_code": "buy",  
          "symbol": "nvda",  
          "price": "12.7330024299341033611199236474931240081787109375",  
          "total": "15241.40390863112172326054861"  
        },  
        {  
           "date": {"$date": 1465776000000},  
           "amount": 8797,  
           "transaction_code": "buy",  
           "symbol": "nvda",  
           "price": "46.53873172406391489630550495348870754241943359375",  
           "total": "409401.2229765902593427995271"  
        },  
        {  
           "date": {"$date": 1472601600000},  
           "amount": 6146,  
           "transaction_code": "sell",  
           "symbol": "ebay",  
           "price": "32.11600884852845894101847079582512378692626953125",  
           "total": "197384.9903830559086514995215"  
        },  
        {  
           "date": {"$date": 1101081600000},  
           "amount": 253,  
           "transaction_code": "buy",  
           "symbol": "amzn",  
           "price": "37.77441226157566944721111212857067584991455078125",  
           "total": "9556.926302178644370144411369"  
        },  
        {  
           "date": {"$date": 1022112000000},  
           "amount": 4521,  
           "transaction_code": "buy",  
           "symbol": "nvda",  
           "price": "10.763069758141103449133879621513187885284423828125",  
           "total": "48659.83837655592869353426977"  
        },  
        {  
           "date": {"$date": 936144000000},  
           "amount": 955,  
           "transaction_code": "buy",  
           "symbol": "csco",  
           "price": "27.992136535152877030441231909207999706268310546875",  
           "total": "26732.49039107099756407137647"  
        }  
      ]  
    }  
  
← Sample AirBnB Listings DatasetSample Geospatial Dataset →

