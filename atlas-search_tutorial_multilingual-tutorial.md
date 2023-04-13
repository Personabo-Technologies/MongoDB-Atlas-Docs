Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# How to Run Multilingual Atlas Search Queries

Select your language

MongoDB Shell

On this page

  * Create the Atlas Search Index
  * Search the Collection

This tutorial describes how to create an index that uses a language analyzer
and perform a multilingual search against the `sample_mflix.movies`
collection. It takes you through the following steps:

  1. Set up an Atlas Search index with dynamic mapping for the `sample_mflix.movies` collection. You can apply the `lucene.italian` language analyzer or the `lucene.italian` and `lucene.english` language analyzer for indexing the `fullplot` field. Atlas Search uses the default `lucene.standard` analyzer for all the other fields that it dynamically indexes in the collection.

  2. Run an Atlas Search compound query against the `fullplot`, `released`, and `genres` fields in the `sample_mflix.movies` collection.

Before you begin, ensure that your Atlas cluster meets the requirements
described in the Prerequisites.

## Create the Atlas Search Index

In this section, you will create an Atlas Search index on the `fullplot` field
in the `sample_mflix.movies` collection.

1

### Navigate to the Atlas Search page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click your cluster's name.

  4. Click the Search tab.

2

### Click Create Index.

3

### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

  * To edit the raw index definition, select JSON Editor.

4

### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter `default`.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the `sample_mflix` database, and select the `movies` collection.

5

### Specify an index definition.

You can use the Visual Editor or the JSON Editor in the Atlas user interface
to create the index. You can set up the index to analyze the `fullplot` field
using the Italian language only or using both Italian and English languages.

Visual Editor

JSON Editor

  1. Click Refine Your Index.

  2. In the Field Mappings section, click Add Field to display the Add Field Mapping window.

  3. Select `fullplot` for the Field Name.

  4. In the settings for the data type, you can configure whether to analyze the field using the Italian language only or using both Italian and English languages.

Italian

Italian and English

    1. Click the Data Type dropdown and select String.

    2. Modify the the Index Analyzer and Search Analyzer to use `lucene.italian` analyzer.

      1. From the Index Analyzer dropdown, select `lucene.language` and then `lucene.italian`.

      2. If Search Analyzer didn't automatically update, from the Search Analyzer dropdown, select `lucene.language` and then `lucene.italian`.

  5. Click Add.

  6. In the Index Configurations section, ensure the following settings and make changes if needed:

    * Use `lucene.standard` for Index Analyzer and Search Analyzer

    * Enable Dynamic Mapping

  7. Click Save Changes.

6

### Click Create Search Index.

7

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

8

### Wait for the index to finish building.

The index should take about one minute to build. While it is building, the
Status column reads `Build in Progress`. When it is finished building, the
Status column reads `Active`.

## Search the Collection

* * *

➤ Use the **Select your language** drop-down menu to set the language of the
example in this section.

* * *

You can use the compound operator to combine two or more operators into a
single query. In this section, connect to your Atlas cluster and the run the
sample query against the `sample_mflix.movies` collection using the `compound`
operator.

MongoDB Shell

Compass

C#

Go

Java (Sync)

Node.js

Python

Italian

Italian and English

1

### Connect to your cluster in `mongosh`.

Open `mongosh` in a terminal window and connect to your cluster. For detailed
instructions on connecting, see Connect via `mongosh`.

2

### Use the `sample_mflix` database.

Run the following command at `mongosh` prompt:

    
    
    use sample_mflix  
      
  
MongoDB Shell

3

### Run an Atlas Search multilingual query that searches for an Italian term.

This query uses the following `compound` operator clauses to query the
collection:

  * `must` clause to search for movie plots in Italian that contain the term `coppia` with the text operator

  * `mustNot` clause to exclude movies released between the years 2000 to 2009 using the range operator

  * `should` clause to specify preference for the `Drama` genre with the text operator

The query uses the $project pipeline stage to:

  * Exclude all fields except `title`, `fullplot`, `released`, and `genres`

  * Add a field named `score`

    
    
    db.movies.aggregate([   
      
      {   
        $search: {   
          "compound": {  
            "must": [{   
              "text": {   
                "path": "fullplot",   
                "query":  "coppia"  
              }  
            }],   
            "mustNot": [{   
              "range": {   
                "path": "released",   
                "gt": ISODate("2000-01-01T00:00:00.000Z"),   
                "lt": ISODate("2009-01-01T00:00:00.000Z")   
              }   
            }],   
            "should": [{   
              "text": {   
                "query": "Drama",   
                "path": "genres"   
              }   
            }]   
          }  
        }  
      },   
      {   
        $project: {   
          "_id": 0,   
          "title": 1,   
          "fullplot": 1,   
          "released": 1,   
          "genres": 1,   
          "score": {   
            "$meta": "searchScore"   
          }   
        }   
      }  
    ])  
  
MongoDB Shell

The query returns the following results:

    
    
    {  
      
      genres: [ 'Drama' ],  
      title: 'Donzoko',  
      fullplot: `Una coppia di gretti usurai gestisce uno squallido  
      dormitorio, nei pressi di una discarica. Una folla di larve e  
      relitti umani affolla il locale: un ex attore alcolizzato; una  
      prostituta; un fabbro che sragiona; disoccupati ed altri ancora.  
      In tutti c'è la ricerca della fuga dalla loro miseranda esistenza,  
      attraverso alcool, gioco, sogni. Arriva un giorno al dormitorio  
      un vecchio e saggio pellegrino, che porta in tutti una nota di  
      speranza con la sua filosofia e la sua umanitè. Ma il sogno dura  
      poco : lo sconforto torna ad impadronirsi di tutti, al punto da  
      portare l'ex attore al suicidio e gli altri a ribellarsi ai due  
      gestori. Ispirato ad un dramma di Gorkij, il film parla della parte  
      sconfitta dell'umanitè, dei vinti, dei falliti, dei rifiutati  
      dalla  
      societè "civile".`,  
      released: ISODate("1957-10-01T00:00:00.000Z"),  
      score: 4.606284141540527  
    },  
    {  
      genres: [ 'Mystery', 'Thriller' ],  
      title: 'Compartiment tueurs',  
      fullplot: "Sei persone viaggiano in un vagone-letto da Marsiglia a  
      Parigi. All'arrivo, un donna viene trovata morta nella sua cuccetta.  
      La polizia si mette alla ricerca delle altre persone, sospettando  
      possa essere stato uno degli altri cinque passeggeri a commettere  
      l'omicidio, ma questi sono uccisi uno ad uno. Gli ultimi due (una  
      coppia di ragazzi conosciutisi per caso nella carrozza) decidono di  
      cercare di risolvere il caso, per non essere uccisi a loro volta,  
      rischiando comunque di esserlo. Con il loro aiuto il caso viene  
      risolto: un giovane e squattrinato studente, amante di una ricca ed  
      attempata attrice (una delle vittime) ha organizzato gli omicidi  
      con il suo amante, un giovane poliziotto nevrotico, per derubare la  
      donna e fuggire insieme in Africa; per cui bisognava uccidere tutti  
      i componenti del vagone-letto per non destare sospetti. Alla fine,  
      dopo un inseguimento notturno per le vie di Parigi, lo studente  
      viene arrestato ed il complice si suicida per non essere catturato.",  
      released: ISODate("1965-11-17T00:00:00.000Z"),  
      score: 3.9604406356811523  
    }  
  
MongoDB Shell

← How to Use Synonyms with Atlas SearchHow to Define a Custom Analyzer and Run
an Atlas Search Diacritic-Insensitive Query →

