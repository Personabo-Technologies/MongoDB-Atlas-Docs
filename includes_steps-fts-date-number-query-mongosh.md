Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Connect to your cluster using `mongosh`.

Share Feedback

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

# Use the `sample_airbnb` database.

Share Feedback

Run the following command at `mongosh` prompt:

    
    
    use sample_airbnb  
      
  
HIDE OUTPUT

    
    
    switched to db sample_airbnb  
      
  
3

# Run the following Atlas Search queries using the operator for which you
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

    
    
    db.airbnb_mat_view.aggregate([  
      
      {  
        "$search": {  
          "queryString": {  
            "defaultPath": "propertyType",  
            "query": "propertyType: (Apartment OR Condominium) AND accommodatesNumber: 4 AND lastScrapedDate: 2019"  
          }  
        }  
      },  
      { $limit: 5 },  
      {  
        $project: {  
          "_id": 0  
        }  
      }  
    ])  
  
HIDE OUTPUT

    
    
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

