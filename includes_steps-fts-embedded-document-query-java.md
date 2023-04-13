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

# Create files named `BasicEmbeddedDocumentsSearch.java` and
`NestedEmbeddedDocumentsSearch.java`.

Share Feedback

3

# Copy and paste the code for the Atlas Search query into the respective file.

Share Feedback

The following queries search the documents inside the `teachers` array. The
queries use the following pipeline stages:

  * `$search` to search the collection.

  * `$project` to include the `_id` field and all the fields in the `teachers` array of documents, and add a field named `score` in the results.

Basic Search

Nested Array Search

The following query searches at the `teachers` path for teachers with the
first name `John` and specifies a preference for teachers with the last name
`Smith`.

    
    
    import java.util.Arrays;  
      
    import java.util.List;  
      
    import static com.mongodb.client.model.Aggregates.limit;  
    import static com.mongodb.client.model.Aggregates.project;  
    import static com.mongodb.client.model.Projections.*;  
    import com.mongodb.client.MongoClient;  
    import com.mongodb.client.MongoClients;  
    import com.mongodb.client.MongoCollection;  
    import com.mongodb.client.MongoDatabase;  
    import org.bson.Document;  
      
    public class BasicEmbeddedDocumentsSearch {  
      public static void main( String[] args ) {  
        // define clauses  
        List<Document> mustClause =  
            List.of(  
                new Document(  
                		"text",   
                        new Document("path", "teachers.first")  
                            .append("query", "John")));  
        List<Document> shouldClause =  
            List.of(  
                new Document(  
                		"text",   
                        new Document("path", "teachers.last")  
                                .append("query", "Smith")));  
      
        // define query  
        Document agg =  
            new Document(  
                "$search",  
                new Document(  
                		"embeddedDocument",   
                	    new Document("path", "teachers")  
                	        .append("operator",   
                	    new Document("compound",  
                        new Document("must", mustClause)  
                        .append("should", shouldClause)))));  
      
        // specify connection  
        String uri = "<connection-string>";  
      
        // establish connection and set namespace  
        try (MongoClient mongoClient = MongoClients.create(uri)) {  
          MongoDatabase database = mongoClient.getDatabase("local_school_district");  
          MongoCollection<Document> collection = database.getCollection("schools");  
      
          // run query and print results  
          collection.aggregate(Arrays.asList(agg,  
            limit(5),  
            project(fields(excludeId(), include("teachers"), computed("score", new Document("$meta", "searchScore"))))))  
            .forEach(doc -> System.out.println(doc.toJson()));  
        }  
      }  
    }  
  
Before you run the sample, replace `<connection-string>` with your Atlas
connection string. Ensure that your connection string includes your database
user's credentials. To learn more, see Connect via Your Application.

4

# Compile and run the Java file.

Share Feedback

Basic Search

Nested Array Search

    
    
    javac BasicEmbeddedDocumentsSearch.java  
      
    java BasicEmbeddedDocumentsSearch  
  
HIDE OUTPUT

    
    
    1| {  
    |  
    2|     "teachers": [  
    3|         {"first": "Jane", "last": "Earwhacker", "classes": [{"subject": "art", "grade": "9th"}, {"subject": "science", "grade": "12th"}]},   
    4|         {"first": "John", "last": "Smith", "classes": [{"subject": "math", "grade": "12th"}, {"subject": "art", "grade": "10th"}]}  
    5|     ],   
    6|     "score": 0.7830756902694702  
    7| }  
    8| {  
    9|     "teachers": [  
    10|         {"first": "Jane", "last": "Smith", "classes": [{"subject": "science", "grade": "9th"}, {"subject": "math", "grade": "12th"}]},   
    11|         {"first": "John", "last": "Redman", "classes": [{"subject": "art", "grade": "12th"}]}  
    12|     ],   
    13|     "score": 0.468008816242218  
    14| }  
  
The two documents in the results contain teachers with the first name `John`.
The document with `_id: 1` ranks higher because it contains a teacher with the
first name `John` who also has the last name `Smith`.

What is MongoDB Atlas? →

