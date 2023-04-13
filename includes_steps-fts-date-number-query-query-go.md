Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Create a file named `date-number-to-string-query.go`.

Share Feedback

2

# Copy and paste the code example for the operator for which you created the
index into the `date-number-to-string-query.go` file.

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

    
    
    package main  
      
    import (  
    	"context"  
    	"fmt"  
    	"time"  
      
    	"go.mongodb.org/mongo-driver/bson"  
    	"go.mongodb.org/mongo-driver/mongo"  
    	"go.mongodb.org/mongo-driver/mongo/options"  
    )  
      
    func main() {  
    	var err error  
        // connect to the Atlas cluster  
    	ctx := context.Background()  
    	client, err := mongo.Connect(ctx, options.Client().ApplyURI("<connection-string>"))  
    	if err != nil {  
    		panic(err)  
    	}  
    	defer client.Disconnect(ctx)  
    	// set namespace  
    	collection := client.Database("sample_airbnb").Collection("airbnb_mat_view")  
        // define pipeline  
        searchStage := bson.D{{"$search", bson.D{{"queryString", bson.D{  
          {"defaultPath", "propertyType"},  
          {"query", "propertyType: (Apartment OR Condominium) AND accommodatesNumber: 4 AND lastScrapedDate: 2019"},  
        }}}}}  
    	limitStage := bson.D{{"$limit", 5}}  
    	projectStage := bson.D{{"$project", bson.D{{"_id", 0}}}}  
    	// specify the amount of time the operation can run on the server  
        opts := options.Aggregate().SetMaxTime(5 * time.Second)  
    	// run pipeline  
    	cursor, err := collection.Aggregate(ctx, mongo.Pipeline{searchStage, limitStage, projectStage}, opts)  
    	if err != nil {  
    	  panic(err)  
        }  
        // print results  
    	var results []bson.D  
    	if err = cursor.All(context.TODO(), &results); err != nil {  
    		panic(err)  
    	}  
    	for _, result := range results {  
    		fmt.Println(result)  
    	}  
    }  
  
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

    
    
    go run date-number-to-string-query.go  
      
  
HIDE OUTPUT

    
    
    1| [  
    |  
    2|     {lastScrapedDate 2019-03-06}   
    3|     {propertyName LAHAINA, MAUI! RESORT/CONDO BEACHFRONT!! SLEEPS 4!}   
    4|     {propertyType Condominium}   
    5|     {accommodatesNumber 4}   
    6|     {maximumNumberOfNights 1125}  
    7| ]  
    8| [  
    9|     {lastScrapedDate 2019-03-06}   
    10|     {propertyName Makaha Valley Paradise with OceanView}   
    11|     {propertyType Condominium}   
    12|     {accommodatesNumber 4}   
    13|     {maximumNumberOfNights 180}  
    14| ]  
    15| [  
    16|     {lastScrapedDate 2019-03-06}   
    17|     {propertyName March 2019 availability! Oceanview on Sugar Beach!}   
    18|     {propertyType Condominium}   
    19|     {accommodatesNumber 4}   
    20|     {maximumNumberOfNights 1125}  
    21| ]  
    22| [  
    23|     {lastScrapedDate 2019-03-06}   
    24|     {propertyName Tropical Jungle Oasis}   
    25|     {propertyType Condominium}   
    26|     {accommodatesNumber 4}   
    27|     {maximumNumberOfNights 1125}  
    28| ]  
    29| [  
    30|     {lastScrapedDate 2019-02-11}   
    31|     {propertyName Hospede-se com acesso fácil.}   
    32|     {propertyType Condominium}   
    33|     {accommodatesNumber 4}   
    34|     {maximumNumberOfNights 1125}  
    35| ]  
  
What is MongoDB Atlas? →

