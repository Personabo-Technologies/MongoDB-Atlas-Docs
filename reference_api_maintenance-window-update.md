Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Maintenance Window

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Maintenance Window Considerations

Urgent Maintenance Activities

    Urgent maintenance activities such as security patches cannot wait for your chosen window. Atlas will start those maintenance activities when needed.
Ongoing Maintenance Operations

    Once maintenance is scheduled for your cluster, you cannot change your maintenance window until the current maintenance efforts have completed.
Maintenance Requires Replica Set Elections

    Atlas performs maintenance the same way as the maintenance procedure described in the MongoDB Manual. This procedure requires at least one replica set election during the maintenance window per replica set.
Maintenance Starts As Close to the Hour As Possible

    Maintenance always begins as close to the scheduled hour as possible, but in-progress cluster updates or unexpected system issues could delay the start time.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    PATCH /groups/{GROUP-ID}/maintenanceWindow  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier of the project from which you want to retrieve the
Maintenance Window.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

Your request can either start the window immediately ( **startASAP : true** )
or change the maintenance window schedule. To use **startASAP : true** , You
need to have scheduled maintenance and set your own maintenance window.

Schedule Day and Time

Start Now

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
dayOfWeek

|

number

|

Required

|

Day of the week that you want the maintenance window to start, as a 1-based
integer.

|

Day of Week

|

Integer  
  
|  
  
Sunday

|

 **1**  
  
Monday

|

 **2**  
  
Tuesday

|

 **3**  
  
Wednesday

|

 **4**  
  
Thursday

|

 **5**  
  
Friday

|

 **6**  
  
Saturday

|

 **7**  
  
hourOfDay

|

number

|

Required

|

Hour of the day that you want the maintenance window to start. This parameter
uses the 24-hour clock, where midnight is **0** and noon is **12**.  
  
autoDeferOnceEnabled

|

boolean

|

Optional

|

Flag that indicates whether you want to defer all maintenance windows one week
they would be triggered.  
  
## Response

This endpoint returns an empty JSON Object.

## Example Request

Schedule Day and Time

Start Now

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/maintenanceWindow?pretty=true" \  
         --data '  
           {  
             "dayOfWeek" : 1,  
             "hourOfDay" : 12,  
             "autoDeferOnceEnabled" : true  
           }'  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

This endpoint returns an empty JSON Object.

What is MongoDB Atlas? →

