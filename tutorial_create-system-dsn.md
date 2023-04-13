Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a System DSN

Share Feedback

On this page

  * Prerequisites
  * Procedure

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

The following steps describe how to create a system Data Source Name (DSN) for
the BI Connector for Atlas. A DSN is a saved configuration which describes a
database connection to be used by an ODBC driver. Once the DSN is created, you
can configure a wide range of SQL clients and BI tools to use the DSN and
import data from MongoDB.

Windows

macOS

## Prerequisites

Before creating a DSN, you should:

Windows

macOS

  * Download and install Visual C++ Redistributable for Visual Studio 2015

  * Download and install the MongoDB ODBC Driver for BI Connector for your platform.

## Procedure

Windows

macOS

1

### Start the Microsoft ODBC Data Sources program.

Choose the program version (64-bit or 32-bit) which is appropriate for your
system and ODBC driver version.

2

### Select `System DSN`, then click Add.

click to enlarge

3

### Select a MongoDB ODBC driver from the list of available drivers.

Select either the MongoDB ODBC ANSI Driver or the MongoDB ODBC Unicode Driver,
then click OK.

## Note

ANSI ODBC/Connectors offer better performance but have a limited character
set. Unicode ODBC/Connectors support a wider character set but may be less
performant.

4

### Fill in the necessary form fields.

Click the Details button to expose the lower half of the form.

The following form fields are required:

Field Name

|

Description  
  
|  
  
Data Source Name

|

A name of your choice.  
  
TCP/IP Server

|

The hostname specified in the Atlas connect dialog.  
  
Port

|

The IANA port number specified in the Atlas connect dialog. The default is
`27015`.  
  
Database

|

The name of the database to which you want to connect.  
  
User

|

Enter either the user specified in the Atlas connect dialog or another
database user with access to the database.

The user is specified in the following format:

    
    
    | <username>?source=<database-name>  
      
  
where the `<database-name>` is the authentication database for the user. If
`admin` is the authentication database, you can omit `?source=<database-
name>`.

  * If you are using Username and Password (`SCRAM-SHA-256`) authentication, the expected authenticating database is `admin`.

  * If you are using LDAP (`PLAIN`) authentication, the expected authenticating database is `$external`:

## Example

myTestUser?source=$external

  
  
Password

|

The password that corresponds to the specified `User`.  
  
5

### Click Test to validate the ODBC connection.

If the connection is successful, click OK to add the DSN. If the connection
fails, check to make sure your database user is correctly authenticated for
the database named in the connection.

