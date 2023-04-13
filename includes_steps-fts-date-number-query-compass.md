Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Connect to your cluster in MongoDB Compass.

Share Feedback

Open MongoDB Compass and connect to your cluster. For detailed instructions on
connecting, see Connect via Compass.

2

# Use the `airbnb_mat-view` collection in the `sample_airbnb` database.

Share Feedback

On the Database screen, click the `sample_airbnb` database, then click the
`airbnb_mat_view` collection.

3

# Run the following Atlas Search query using the operator for which you
created the index.

Share Feedback

If you created an index that uses dynamic mappings, you can query the
`airbnb_mat_view` collection using the queryString operator. If you created an
index that uses static mappings, you can query the `airbnb_mat_view`
collection using the autocomplete operator.

queryString Operator

autocomplete Operator

AND Query

OR Query

The following query searches for properties where the property type is
`Apartment` or `Condominium`, accommodates `2` people, and was listed in
`2019`.

Pipeline Stage

|

Query  
  
|  
  
`$search`

|

    
    
    | {  
      
      "index": "default",  
      "queryString": {  
        "defaultPath": "propertyType",  
        "query": "propertyType: House OR accommodatesNumber: 2 OR lastScrapedDate: 2019 OR maximumNumberOfNights: 30"  
      }  
    }  
  
`$limit`

|

    
    
    | {  
      
      5  
    }  
  
`$project`

|

    
    
    | {  
      
      "_id": 0  
    }  
  
If you enabled Auto Preview, MongoDB Compass displays the following documents
next to the `$project` pipeline stage:

    
    
    1|   [  
    |  
    2|     {  
    3|       lastScrapedDate: '2019-03-06',  
    4|       propertyName: 'LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!',  
    5|       propertyType: 'Condominium',  
    6|       accommodatesNumber: '4'  
    7|     },  
    8|     {  
    9|       lastScrapedDate: '2019-03-06',  
    10|       propertyName: 'Makaha Valley Paradise with OceanView',  
    11|       propertyType: 'Condominium',  
    12|       accommodatesNumber: '4'  
    13|     },  
    14|     {  
    15|       lastScrapedDate: '2019-03-06',  
    16|       propertyName: 'March 2019 availability! Oceanview on Sugar Beach!',  
    17|       propertyType: 'Condominium',  
    18|       accommodatesNumber: '4'  
    19|     },  
    20|     {  
    21|       lastScrapedDate: '2019-03-06',  
    22|       propertyName: 'Tropical Jungle Oasis',  
    23|       propertyType: 'Condominium',  
    24|       accommodatesNumber: '4'  
    25|     },  
    26|     {  
    27|       lastScrapedDate: '2019-02-11',  
    28|       propertyName: 'Hospede-se com acesso fácil.',  
    29|       propertyType: 'Condominium',  
    30|       accommodatesNumber: '4'  
    31|     }  
    32|   ]  
    33|     
  
What is MongoDB Atlas? →

