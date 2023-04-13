Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Ensure that your `CLASSPATH` contains the following libraries.

Share Feedback

|  
  
|  
  
`junit`

|

4.11 or higher version  
  
`mongodb-driver-sync`

|

4.3.0 or higher version  
  
`slf4j-log4j12`

|

1.7.30 or higher version  
  
2

# Create a file named `DateNumberToStringQuery.java`.

Share Feedback

3

# Copy and paste the code for the operator for which you created the index
into the `DateNumberToStringQuery.java` file.

Share Feedback

If you created an index that uses dynamic mappings, you can query the
`airbnb_mat_view` collection using the queryString operator. If you created an
index that uses static mappings, you can query the `airbnb_mat_view`
collection using the autocomplete operator.

queryString Operator

autocomplete Operator

The code example performs the following tasks:

  * Imports `mongodb` packages and dependencies.

  * Establishes a connection to your Atlas cluster.

  * Iterates over the cursor to print the documents that match the query.

## Note

To run the sample code in your Maven environment, add the following above the
import statements in your file.

    
    
    package com.mongodb.drivers;  
      
  
AND Query

OR Query

The following query searches for properties where the property type is
`Apartment` or `Condominium`, accommodates `2` people, and was listed in
`2019`.

    
    
    import java.util.Arrays;  
      
    import static com.mongodb.client.model.Filters.eq;  
    import static com.mongodb.client.model.Aggregates.limit;  
    import static com.mongodb.client.model.Aggregates.project;  
    import static com.mongodb.client.model.Projections.excludeId;  
    import static com.mongodb.client.model.Projections.fields;  
    import com.mongodb.client.MongoClient;  
    import com.mongodb.client.MongoClients;  
    import com.mongodb.client.MongoCollection;  
    import com.mongodb.client.MongoDatabase;  
    import org.bson.Document;  
      
    public class DateNumberToStringQuery {  
    	public static void main( String[] args ) {  
    		// define query  
    		Document agg = new Document("defaultPath", "propertyType")  
                    .append("query", "propertyType: (Apartment OR Condominium) AND accommodatesNumber: 4 AND lastScrapedDate: 2019");  
    		// specify connection  
    		String uri = "<connection-string>";  
            // establish connection and set namespace  
    		try (MongoClient mongoClient = MongoClients.create(uri)) {  
    			MongoDatabase database = mongoClient.getDatabase("sample_airbnb");  
    			MongoCollection<Document> collection = database.getCollection("airbnb_mat_view");  
    			// run query and print results  
    			collection.aggregate(Arrays.asList(  
    					eq("$search", eq("queryString", agg)),   
    					limit(5),   
    					project(fields(excludeId()) ))  
    			).forEach(doc -> System.out.println(doc.toJson()));	  
    		}  
    	}  
    }  
  
Before you run the sample, replace `<connection-string>` with your Atlas
connection string. Ensure that your connection string includes your database
user's credentials. To learn more, see Connect via Your Application.

4

# Compile and run `DateNumberToStringQuery.java` file.

Share Feedback

queryString Operator

autocomplete Operator

AND Query

OR Query

    
    
    javac DateNumberToStringQuery.java  
      
    java DateNumberToStringQuery  
  
HIDE OUTPUT

    
    
    1| {  
    |  
    2|     "lastScrapedDate": "2019-03-06",   
    3|     "propertyName": "LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!",   
    4|     "propertyType": "Condominium",   
    5|     "accommodatesNumber": "4",   
    6|     "maximumNumberOfNights": "1125"  
    7| }  
    8| {  
    9|     "lastScrapedDate": "2019-03-06",   
    10|     "propertyName": "Makaha Valley Paradise with OceanView",   
    11|     "propertyType": "Condominium",   
    12|     "accommodatesNumber": "4",   
    13|     "maximumNumberOfNights": "180"  
    14| }  
    15| {  
    16|     "lastScrapedDate": "2019-03-06",   
    17|     "propertyName": "March 2019 availability! Oceanview on Sugar Beach!",   
    18|     "propertyType": "Condominium",   
    19|     "accommodatesNumber": "4",   
    20|     "maximumNumberOfNights": "1125"  
    21| }  
    22| {  
    23|     "lastScrapedDate": "2019-03-06",   
    24|     "propertyName": "Tropical Jungle Oasis",   
    25|     "propertyType": "Condominium",   
    26|     "accommodatesNumber": "4",   
    27|     "maximumNumberOfNights": "1125"  
    28| }  
    29| {  
    30|     "lastScrapedDate": "2019-02-11",   
    31|     "propertyName": "Hospede-se com acesso fácil.",   
    32|     "propertyType": "Condominium",   
    33|     "accommodatesNumber": "4",   
    34|     "maximumNumberOfNights": "1125"  
    35| }  
  
What is MongoDB Atlas? →

