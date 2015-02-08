Curation Dashboard Public API
======
Requirements
======
Format
---
The Curation Dashboard Public API can be accessed via the following base URI

`https://dashboard.curationcorp.com/api/1`

All routes given in this documentation are relative to this base route. Note that unlike the Dashboard itself, the Public API only accepts connections over `https://`. 

All responses are given in `JSON`. 

Authentication
----
Curation Dashboard's Public API uses HTTP Basic Access Authentication to ensure only correctly permissioned users are given access to the feeds they are allowed to read. 

Each API call made to Curation Dashboard is authenticated with a key generated on a per-user basis. Users' keys may be found on their profile page after logging in to Dashboard. 
This key is included in the HTTP header in the call made as follows: 

```Authorization: Token [INSERT KEY HERE]```

To prevent abuse, we require you to enter the public IP of the servers you wish to interface with the API in your profile. 

Endpoints
=====

Listing Available Feeds
----
####`/widgets`
An authenticated user that has been granted access to the REST API can list the feeds they are permissioned on by issuing a GET request to `/widgets`.  A `200 ` response will be issued along with a JSON object of widgets, as follows: 
```
{
	"widgets" : {
	"Interoperability" : "",
	"Healthcare Costs" : "", 
	"Healthcare News" : "", 
	"Autism": ""
	}
}
```
The Key corresponds to the human-readable name of the feed, and the value corresponds to the unique identifier of the feed, or widget ID. 

Retrieving items from feeds
----
####`/widgets/items/:widgetID[s]`
An authenticated user can retrieve items from a feed/feeds by issuing an HTTP GET request to `/widgets/items/` along with the relevant widget IDs, retrieved from `/widgets`. A user can issue many requests with a single ID or one request with many comma-separated IDs, for example: 
   
	GET /widgets/items/abc,123,def,456

A successful request will return a `200` response along with a JSON object with an array of items from the requested widgets, ordered by descending date, as follows: 

|Property Name | Type | Description |
|--------------|------|------------|
|`title` | *string* |The title text of an item.|
|`searchtext` | *string* | An extract of the item.|
|`thumbnailUrl`| [optional] *string* | A URL to an image of the item. This is a hotlink to the original image from the source. |
|`date` | *string* | word |
|`link` | *string* | A link to the item. |
|`source`| *string* |A human readable name of the item's source.|

```
{
	"title": "", 
	"searchtext": "", 
	"thumbnailUrl": "",
	"date": "",
	"link": ""
	"sourceName": "", 
	"sourceUrl": "", 
	"widgetID": "" 
}
```






