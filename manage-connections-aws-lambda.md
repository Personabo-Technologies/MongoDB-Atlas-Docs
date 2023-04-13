Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Connections with AWS Lambda

Select your language

C#

On this page

  * Best Practices
  * Connection Example
  * AWS IAM Authentication
  * Other Authentication
  * AWS IAM Authentication
  * Other Authentication
  * AWS IAM Authentication
  * Other Authentication

## Best Practices

Use the following best practices to properly manage connections between AWS
Lambda and Atlas:

  * Define the client to the MongoDB server outside the AWS Lambda handler function.

Don't define a new MongoClient object each time you invoke your function.
Doing so causes the driver to create a new database connection with each
function call. This can be expensive and can result in your application
exceeding database connection limits. As an alternative, do the following:

    1. Create the MongoClient object once.

    2. Store the object so your function can reuse the MongoClient across function invocations.

The Connection Example reuses existing database connections to speed up
communication with the database and keep connection counts to the database at
a reasonable level with respect to application traffic.

C#

Go

Java (Sync)

Node.js

Python

Ruby

  * Restrict network access to your Atlas cluster.

Connect to your Atlas cluster over private networking using a Network Peering
connection between your Atlas cluster and your AWS Lambda function, or,
alternatively, a private endpoint, so that you can allow only private IP
addresses to your IP access list.

If private networking is not an option, consider connecting to your Atlas
cluster via a NAT gateway with a mapped Elastic IP address. Otherwise, you
must allow all IP addresses (0.0.0.0/0) to access your service cluster.

## Warning

Adding `0.0.0.0/0` to your IP access list allows cluster access from anywhere
in the public internet. Ensure that you're using strong credentials for all
database users when allowing access from anywhere.

  * Set Up Unified AWS Access and use AWS IAM authentication where possible.

You can connect to your Atlas clusters using AWS IAM roles instead of
hardcoding your credentials in Lambda. Hardcoded credentials are viewable by
anyone who accesses your AWS Lambda environment, which can pose a security
risk. With AWS IAM authentication, Atlas accesses AWS Lambda through an
assumed IAM role, so you don't need credentials in your connection strings.

Atlas supports AWS IAM authentication for clusters running MongoDB version 4.4
or higher. We strongly advise using AWS IAM authentication for Lambda
connections if your cluster meets the requirements.

## Connection Example

C#

Go

Java (Sync)

Node.js

Python

Ruby

### AWS IAM Authentication

    
    
    string username = Environment.GetEnvironmentVariable("AWS_ACCESS_KEY_ID");  
      
    string password = Environment.GetEnvironmentVariable("AWS_SECRET_ACCESS_KEY");  
    string awsSessionToken = Environment.GetEnvironmentVariable("AWS_SESSION_TOKEN");  
      
    var awsCredentials =  
        new MongoCredential("MONGODB-AWS", new MongoExternalIdentity(username), new PasswordEvidence(password))  
        .WithMechanismProperty("AWS_SESSION_TOKEN", awsSessionToken);  
      
    var mongoUrl = MongoUrl.Create($"<MONGODB_URI>");  
      
    var mongoClientSettings = MongoClientSettings.FromUrl(mongoUrl);  
    mongoClientSettings.Credential = awsCredentials;  
    mongoClientSettings.ServerApi = new ServerApi(ServerApiVersion.V1, strict: true);  
      
    return new MongoClient(mongoClientSettings);  
  
C#

### Other Authentication

    
    
    private static MongoClient MongoClient { get; set; }  
      
    private static MongoClient CreateMongoClient()  
    {  
        var mongoClientSettings = MongoClientSettings.FromConnectionString($"<MONGODB_URI>");  
        mongoClientSettings.ServerApi = new ServerApi(ServerApiVersion.V1, strict: true);  
        return new MongoClient(mongoClientSettings);  
    }  
      
    static ShareMongoClientLambdaHandler()  
    {  
        MongoClient = CreateMongoClient();  
    }  
      
    public string HandleRequest(ILambdaContext context)  
    {  
        var database = MongoClient.GetDatabase("db");  
        var collection = database.GetCollection<BsonDocument>("coll");  
        var result = collection.Find(FilterDefinition<BsonDocument>.Empty).First();  
        return result.ToString();  
    }  
  
C#

← Simulate Regional OutageTroubleshoot Connection Issues →

