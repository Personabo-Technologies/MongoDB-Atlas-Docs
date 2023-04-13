Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Cloud Provider Regions

Share Feedback

On this page

  * Required Roles
  * Request
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

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

To use this resource, your API Key must have the `Project Read Only` role.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/provider/regions?providers={CLOUD-PROVIDER}&tier={CLUSTER-TIER}  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

Required

|

string

|

Unique identifier for the project containing the cloud provider regions and
cluster tiers you want to retrieve.  
  
### Request Query Parameters

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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
|

|

|  
  
|||  
  
providers

|

string

|

Optional

|

Cloud providers whose regions to retrieve. Allowable values include `AWS`,
`GCP`, and `AZURE`. When you specify multiple providers, response is limited
to tiers and regions that support multi-cloud clusters.  
  
tier

|

string

|

Optional

|

Cluster tier for which to retrieve the regions. To learn more about cluster
tiers, see Select Cluster Tier.  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response

|

|  
  
||  
  
instanceSizes

|

array

|

List of instances sizes that this cloud provider supports.  
  
instanceSizes[n].availableRegions

|

array

|

List of regions that this cloud provider supports for this instance size.  
  
instanceSizes[n].availableRegions[m].default

|

Boolean

|

Flag that indicates whether the cloud provider sets this region as its
default.

  *  **AWS** defaults to **US_EAST_1**.

  *  **GCP** defaults to **CENTRAL_US**.

  *  **AZURE** defaults to **US_WEST_2**.

  
  
instanceSizes[n].availableRegions[m].name

|

string

|

Label that identifies the supported region.

 **See also:**

  * AWS regions

  * GCP regions

  * Azure regions

  
  
instanceSizes[n].name

|

string

|

Label that identifies the instance size or cluster tier.  
  
provider

|

string

|

Cloud providers that the response includes. Allowable values include **AWS** ,
**GCP** , and **AZURE**.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0//groups/{GROUP-ID}/clusters/provider/regions?providers=AZURE&providers=AWS&tier=M10?pretty=true"  
  
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

    
    
    1| {  
    |  
    2|   "links": [  
    3|     {  
    4|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/provider/regions?providers=AZURE&providers=AWS&tier=M10&pageNum=1&itemsPerPage=100",  
    5|       "rel": "self"  
    6|     }  
    7|   ],  
    8|   "results": [  
    9|     {  
    10|       "instanceSizes": [  
    11|         {  
    12|           "availableRegions": [  
    13|             {  
    14|               "default": false,  
    15|               "name": "US_CENTRAL"  
    16|             },  
    17|             {  
    18|               "default": false,  
    19|               "name": "US_EAST"  
    20|             },  
    21|             {  
    22|               "default": false,  
    23|               "name": "US_EAST_2"  
    24|             },  
    25|             {  
    26|               "default": false,  
    27|               "name": "US_NORTH_CENTRAL"  
    28|             },  
    29|             {  
    30|               "default": false,  
    31|               "name": "US_WEST"  
    32|             },  
    33|             {  
    34|               "default": false,  
    35|               "name": "US_SOUTH_CENTRAL"  
    36|             },  
    37|             {  
    38|               "default": false,  
    39|               "name": "EUROPE_NORTH"  
    40|             },  
    41|             {  
    42|               "default": false,  
    43|               "name": "EUROPE_WEST"  
    44|             },  
    45|             {  
    46|               "default": false,  
    47|               "name": "US_WEST_CENTRAL"  
    48|             },  
    49|             {  
    50|               "default": true,  
    51|               "name": "US_WEST_2"  
    52|             },  
    53|             {  
    54|               "default": false,  
    55|               "name": "CANADA_EAST"  
    56|             },  
    57|             {  
    58|               "default": false,  
    59|               "name": "CANADA_CENTRAL"  
    60|             },  
    61|             {  
    62|               "default": false,  
    63|               "name": "BRAZIL_SOUTH"  
    64|             },  
    65|             {  
    66|               "default": false,  
    67|               "name": "AUSTRALIA_EAST"  
    68|             },  
    69|             {  
    70|               "default": false,  
    71|               "name": "AUSTRALIA_SOUTH_EAST"  
    72|             },  
    73|             {  
    74|               "default": false,  
    75|               "name": "UAE_NORTH"  
    76|             },  
    77|             {  
    78|               "default": false,  
    79|               "name": "GERMANY_WEST_CENTRAL"  
    80|             },  
    81|             {  
    82|               "default": false,  
    83|               "name": "GERMANY_NORTH"  
    84|             },  
    85|             {  
    86|               "default": false,  
    87|               "name": "SWITZERLAND_NORTH"  
    88|             },  
    89|             {  
    90|               "default": false,  
    91|               "name": "SWITZERLAND_WEST"  
    92|             },  
    93|             {  
    94|               "default": false,  
    95|               "name": "UK_SOUTH"  
    96|             },  
    97|             {  
    98|               "default": false,  
    99|               "name": "UK_WEST"  
    100|             },  
    101|             {  
    102|               "default": false,  
    103|               "name": "INDIA_CENTRAL"  
    104|             },  
    105|             {  
    106|               "default": false,  
    107|               "name": "INDIA_WEST"  
    108|             },  
    109|             {  
    110|               "default": false,  
    111|               "name": "INDIA_SOUTH"  
    112|             },  
    113|             {  
    114|               "default": false,  
    115|               "name": "ASIA_EAST"  
    116|             },  
    117|             {  
    118|               "default": false,  
    119|               "name": "JAPAN_EAST"  
    120|             },  
    121|             {  
    122|               "default": false,  
    123|               "name": "JAPAN_WEST"  
    124|             },  
    125|             {  
    126|               "default": false,  
    127|               "name": "ASIA_SOUTH_EAST"  
    128|             },  
    129|             {  
    130|               "default": false,  
    131|               "name": "KOREA_CENTRAL"  
    132|             },  
    133|             {  
    134|               "default": false,  
    135|               "name": "KOREA_SOUTH"  
    136|             },  
    137|             {  
    138|               "default": false,  
    139|               "name": "FRANCE_CENTRAL"  
    140|             },  
    141|             {  
    142|               "default": false,  
    143|               "name": "SOUTH_AFRICA_NORTH"  
    144|             },  
    145|             {  
    146|               "default": false,  
    147|               "name": "NORWAY_EAST"  
    148|             },  
    149|             {  
    150|               "default": false,  
    151|               "name": "UAE_CENTRAL"  
    152|             }  
    153|           ],  
    154|           "name": "M10"  
    155|         }  
    156|       ],  
    157|       "provider": "AZURE"  
    158|     },  
    159|     {  
    160|       "instanceSizes": [  
    161|         {  
    162|           "availableRegions": [  
    163|             {  
    164|               "default": true,  
    165|               "name": "US_EAST_1"  
    166|             },  
    167|             {  
    168|               "default": false,  
    169|               "name": "US_EAST_2"  
    170|             },  
    171|             {  
    172|               "default": false,  
    173|               "name": "US_WEST_1"  
    174|             },  
    175|             {  
    176|               "default": true,  
    177|               "name": "US_WEST_2"  
    178|             },  
    179|             {  
    180|               "default": false,  
    181|               "name": "CA_CENTRAL_1"  
    182|             },  
    183|             {  
    184|               "default": false,  
    185|               "name": "EU_NORTH_1"  
    186|             },  
    187|             {  
    188|               "default": false,  
    189|               "name": "EU_WEST_1"  
    190|             },  
    191|             {  
    192|               "default": false,  
    193|               "name": "EU_WEST_2"  
    194|             },  
    195|             {  
    196|               "default": false,  
    197|               "name": "EU_WEST_3"  
    198|             },  
    199|             {  
    200|               "default": false,  
    201|               "name": "EU_CENTRAL_1"  
    202|             },  
    203|             {  
    204|               "default": false,  
    205|               "name": "SA_EAST_1"  
    206|             },  
    207|             {  
    208|               "default": false,  
    209|               "name": "AP_EAST_1"  
    210|             },  
    211|             {  
    212|               "default": false,  
    213|               "name": "AP_SOUTHEAST_2"  
    214|             },  
    215|             {  
    216|               "default": false,  
    217|               "name": "AP_NORTHEAST_1"  
    218|             },  
    219|             {  
    220|               "default": false,  
    221|               "name": "AP_NORTHEAST_2"  
    222|             },  
    223|             {  
    224|               "default": false,  
    225|               "name": "AP_SOUTHEAST_1"  
    226|             },  
    227|             {  
    228|               "default": false,  
    229|               "name": "AP_SOUTH_1"  
    230|             },  
    231|             {  
    232|               "default": false,  
    233|               "name": "ME_SOUTH_1"  
    234|             },  
    235|             {  
    236|               "default": false,  
    237|               "name": "AF_SOUTH_1"  
    238|             },  
    239|             {  
    240|               "default": false,  
    241|               "name": "EU_SOUTH_1"  
    242|             }  
    243|           ],  
    244|           "name": "M10"  
    245|         }  
    246|       ],  
    247|       "provider": "AWS"  
    248|     }  
    249|   ],  
    250|   "totalCount": 2  
    251| }  
  
What is MongoDB Atlas? →

