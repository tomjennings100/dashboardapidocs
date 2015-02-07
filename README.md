Curation Dashboard Public API
======
API
---
The Curation Dashboard Public API can be accessed via the following base URI

`http://dashboard.curationcorp.com/api/1`

All routes given in this documentation are relative to this base route. 

Authentication
----
Curation Dashboard's Public API uses HTTP Basic Access Authentication to ensure only correctly permissioned users are given access to the feeds they are allowed to read. 

Each API call made to Curation Dashboard is authenticated with a key generated on a per-user basis. Users' keys may be found on their profile page after logging in to Dashboard. 
This key is included in the HTTP header in the call made as follows: 

```Authorization: Basic [INSERT KEY HERE]```

Listing Available Feeds
----
####`/widgets`
An authenticaed user that has been granted access to the REST API can list the feeds they are permissioned on by issuing a GET request to `/widgets`.  A `200 ` response will be issued along with a JSON object of widgets, as follows: 
```
{
	"widgets" : {
	"Interoperability" : "",
	"Healthcare Costs" : "", 
	"Healthcare News" : "", 
	"Autism": ""
	}
}```
The Key corresponds to the human-readable name of the dfeed, and the value corresponds to the unique identifier of the feed, or widget ID. 

Retreiving items from feeds
----
####`/widgets/items/:widgetID[s]`
An authenticated user can retrieve items from a feed/feeds by issuing an HTTP GET request to `/widgets/items/` along with the relevant widget IDs, retreived from `/widgets`. A user can issue many requests with a single ID or one request with many comma-separated IDs, for example: 
   
    `GET /widgets/items/abc,123,def,456`

A successful request will return a `200` response along with a JSON object with an array of items from the requested widgets, ordered by descending date, as follows: 

```
{
	"title": "", 
	"content": "", 
	"thumbnailURL": "",
	"date": "",
	"widgetID": "" 
}```





