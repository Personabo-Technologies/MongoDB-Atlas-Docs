Docs Home → Launch & Manage MongoDB → MongoDB Atlas

1

# Create a new directory called `date-number-to-string-query` and initialize
your project with the `dotnet new` command.

Share Feedback

    
    
    mkdir date-number-to-string-query  
      
    cd date-number-to-string-query  
    dotnet new console  
  
2

# Add the .NET/C# Driver to your project as a dependency.

Share Feedback

    
    
    dotnet add package MongoDB.Driver  
      
  
3

# Replace the contents of the `Program.cs` file with the following code for
the operator for which you created the index and the type of query you wish to
run.

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

AND Query

OR Query

The following query searches for properties where the property type is
`Apartment` or `Condominium`, accommodates `2` people, and was listed in
`2019`.

    
    
    using MongoDB.Bson;  
      
    using MongoDB.Bson.Serialization.Attributes;  
    using MongoDB.Bson.Serialization.Conventions;  
    using MongoDB.Driver;  
    using MongoDB.Driver.Search;  
         
    public class DateNumberToStringQuery  
    {  
        private static IMongoCollection<matViewDocument> matViewCollection;  
        private static string _mongoConnectionString = "<connection-string>";  
    	  
        public static void Main(string[] args)  
        {  
            // allow automapping of the camelCase database fields to our MovieDocument  
            var camelCaseConvention = new ConventionPack { new CamelCaseElementNameConvention() };  
            ConventionRegistry.Register("CamelCase", camelCaseConvention, type => true);  
      
            // connect to your Atlas cluster  
            var mongoClient = new MongoClient(_mongoConnectionString);  
            var airbnbDatabase = mongoClient.GetDatabase("sample_airbnb");  
            matViewCollection = airbnbDatabase.GetCollection<matViewDocument>("airbnb_mat_view");  
      
            // define and run pipeline  
            var results = matViewCollection.Aggregate()  
                .Search(Builders<matViewDocument>.Search.QueryString(  
                    airbnb => airbnb.propertyType,   
                    "(Apartment OR Condominium) AND accommodatesNumber: 4 AND lastScrapedDate: 2019"  
                    ))  
                .Limit(5)  
                .Project<matViewDocument>(Builders<matViewDocument>.Projection  
                    .Exclude(airbnb => airbnb.Id))  
                .ToList();  
      
            // print results  
            foreach (var airbnb in results)   
            {  
                Console.WriteLine(airbnb.ToJson());  
            }  
        }  
    }  
      
    [BsonIgnoreExtraElements]  
    public class matViewDocument   
    {  
        [BsonIgnoreIfDefault]  
        public string Id { get; set; }  
        public string lastScrapedDate { get; set; }  
        public string propertyName { get; set; }  
        public string propertyType { get; set; }  
        public string accommodatesNumber { get; set; }  
        public string maximumNumberOfNights { get; set; }  
    }  
  
Before you run the sample, replace `<connection-string>` with your Atlas
connection string. Ensure that your connection string includes your database
user's credentials. To learn more, see Connect via Your Application.

4

# Compile and run the `Program.cs` file.

Share Feedback

queryString Operator

autocomplete Operator

AND Query

OR Query

    
    
    dotnet run Program.cs  
      
  
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

