Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Create a file named `date-number-to-string-query.js`.

Share Feedback

2

# Copy and paste the code for the operator for which you created the index
into the `date-number-to-string-query.js` file.

Share Feedback

If you created an index that uses dynamic mappings, you can query the
`airbnb_mat_view` collection using the queryString operator. If you created an
index that uses static mappings, you can query the `airbnb_mat_view`
collection using the autocomplete operator.

queryString Operator

autocomplete Operator

The code example performs the following tasks:

  * Imports `mongodb`, MongoDB's `Node.js` driver.

  * Creates an instance of the MongoClient class to establish a connection to your Atlas cluster.

  * Iterates over the cursor to print the documents that match the query.

AND Query

OR Query

The following query searches for properties where the property type is
`Apartment` or `Condominium`, accommodates `2` people, and was listed in
`2019`.

    
    
    const MongoClient = require("mongodb").MongoClient;  
      
    const assert = require("assert");  
      
    const agg = [  
      {  
        '$search': {  
          'queryString': {  
            'defaultPath': 'propertyType',  
            'query': 'propertyType: (Apartment OR Condominium) AND accommodatesNumber: 4 AND lastScrapedDate: 2019'  
          }  
        }  
      }, {  
        '$limit': 5  
      }, {  
        '$project': {  
          '_id': 0  
        }  
      }  
    ];  
      
    MongoClient.connect(  
      "<connection-string>",  
      { useNewUrlParser: true, useUnifiedTopology: true },  
      async function (connectErr, client) {  
        assert.equal(null, connectErr);  
        const coll = client.db("sample_airbnb").collection("airbnb_mat_view");  
        let cursor = await coll.aggregate(agg);  
        await cursor.forEach((doc) => console.log(doc));  
        client.close();  
      }  
    );  
  
Before you run the sample, replace `<connection-string>` with your Atlas
connection string. Ensure that your connection string includes your database
user's credentials. To learn more, see Connect via Your Application.

3

# Run the following command to query your collection:

Share Feedback

queryString Operator

autocomplete Operator

AND Query

OR Query

    
    
    node date-number-to-string-query.js  
      
  
HIDE OUTPUT

    
    
    1|   {  
    |  
    2|     lastScrapedDate: '2019-03-06',  
    3|     propertyName: 'LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!',  
    4|     propertyType: 'Condominium',  
    5|     accommodatesNumber: '4',  
    6|     maximumNumberOfNights: '1125'  
    7|   }  
    8|   {  
    9|     lastScrapedDate: '2019-03-06',  
    10|     propertyName: 'Makaha Valley Paradise with OceanView',  
    11|     propertyType: 'Condominium',  
    12|     accommodatesNumber: '4',  
    13|     maximumNumberOfNights: '180'  
    14|   }  
    15|   {  
    16|     lastScrapedDate: '2019-03-06',  
    17|     propertyName: 'March 2019 availability! Oceanview on Sugar Beach!',  
    18|     propertyType: 'Condominium',  
    19|     accommodatesNumber: '4',  
    20|     maximumNumberOfNights: '1125'  
    21|   }  
    22|   {  
    23|     lastScrapedDate: '2019-03-06',  
    24|     propertyName: 'Tropical Jungle Oasis',  
    25|     propertyType: 'Condominium',  
    26|     accommodatesNumber: '4',  
    27|     maximumNumberOfNights: '1125'  
    28|   }  
    29|   {  
    30|     lastScrapedDate: '2019-02-11',  
    31|     propertyName: 'Hospede-se com acesso fácil.',  
    32|     propertyType: 'Condominium',  
    33|     accommodatesNumber: '4',  
    34|     maximumNumberOfNights: '1125'  
    35|   }  
    36|     
  
What is MongoDB Atlas? →

