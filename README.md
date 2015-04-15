Curation Dashboard Public API
======
---
Requirements
======
Administration
---
Administration of API keys is handled by administrators of the Curation Dashboard system, if you would like a further API key, please contact [dashboard@curationcorp.com](mailto:dashboard@curationcorp.com). 

Users with access to the API are given API access to certain widgets within the Dashboard by administrators. 

Format
---
The Curation Dashboard Public API can be accessed via the following base URI

`https://polka-api.curationcorp.com/polka`

All routes given in this documentation are relative to this base route. Note that unlike the Dashboard itself, the Public API only accepts connections over `https://`. 

All responses are given in `JSON`. 

Authentication
----
Curation Dashboard's Public API uses HTTP Basic Access Authentication to ensure only correctly permissioned users are given access to the feeds they are allowed to read. 

Each API call made to Curation Dashboard is authenticated with a key generated on a per-user basis. Curation will provide you with an API key. 

This key is included in the HTTP header in the call made as follows: 

```Authorization: Token [INSERT API KEY]```

<!-- To prevent abuse, we require you to enter the public IP of the servers you wish to interface with the API in your profile.  -->

Endpoints
=====

Listing Available Feeds
----
####`/widgets`
An authenticated user that has been granted access to the REST API can list the feeds they are permissioned on by issuing a GET request to `/widgets`.  A `200 ` response will be issued along with an array of widgets, as follows: 
```
{
    "Widgets": {
        "displayName": "Widgets",
        "values": [
            {
                "Lorem RSS": "54591d9275001d7d14fa3416"
            }
        ]
    }
}
```
The Key corresponds to the human-readable name of the feed, and the value corresponds to the unique identifier of the feed, or widget ID. 

Retrieving items from feeds
----
####`/widget/:widgetId`
An authenticated user can retrieve items from a feed/feeds by issuing an HTTP GET request to `/widget/:widgetId/` along with the relevant widget IDs, retrieved from `/widget`. A user can issue many requests with a single ID or one request with many comma-separated IDs, for example: 
   
	GET /widget/:widgetId

A successful request will return a `200` response along with a JSON object with an array of items from the requested widget, ordered by descending date, as follows: 

|Property | Type | Description |
|--------------|------|------------|
|`title` | *string* |The title text of an item.|
|`description` | *string* | An extract of the item.|
|`published` | *string* | The UTC publish date and time of the item, in ISO 8601 format. If the publish date is not available, this reverts to the date the item arrived in the database.  |
|`link` | *string* | A link to the item. |
|`enclosures`| *array* | An arrary of objects that include a hotlink to image files associated with the item (`url`) and the filetype of the image (`type`. This array is reserved for future expansion to include other media, though currently just serves images |
---
***An example response object***

```
{
    "Items": {
        "displayName": "Items",
        "widgetId": "54591d9275001d7d14fa3416",
        "values":[
		    "_id": "54eaff6fd90478e413fd0add",
		    "link": "http://example.com/test/1424686920",
		    "description": "Adipisicing elit aliqua occaecat occaecat Lorem duis et ullamco duis adipisicing.",
		    "title": "Lorem ipsum 2015-02-23T10:22:00+00:00",
		    "published": "2015-02-23T10:22:00.000Z",
		    "enclosures": [
                    "url": "http://assets.fiercemarkets.net/public/opengraphimages/updated/opengraph_fiercemedicaldevices.jpg",
                    "type": "image/jpeg"
                    ]
		    ]
	    }
	}
}
```
Listing Available Dashboards
----
####`/dashboards`
An authenticated user that has been granted access to the REST API can list the dashboards they are permissioned on by issuing a GET request to `/dashboards`.  A `200 ` response will be issued along with an array of dashboards, as follows: 
```
{
    "Dashboards": {
        "displayName": "Dashboards",
        "values": [
            {
                _id: "54591d9275001d7d14fa3416",
                user: "54591d9275001d7d14fa3416",
                widgets: [
                "54591d9275001d7d14fa3416",
                "54591d9275001d7d14fa3416"
                ]
            }
        ]
    }
}
```
Listing a single Dashboard
----
####`/dashboard/:dashboardId`
An authenticated user that has been granted access to the REST API can get a dashboard and the complete data associated with the dashboard by issuing a GET request to `/dashboard/:dashboardId`.  A `200 ` response will be issued along with dashboard and its data, as follows: 
```
{
    Dashboard: {
        displayName: "Dashboard",
        dashboardId: "54591d9275001d7d14fa3416",
        values: {
            __v: 0,
            _id: "54591d9275001d7d14fa3416",
            columns: 5,
            user: "54591d9275001d7d14fa3416",
            panel: {
                name: "6 Column Panel",
                layout: [
                    [{
                        exp: 2,
                        open: false,
                        tot: 4,
                        widgetid: "",
                        keywords: [],
                        header: "Oil and Gas",
                        content: "",
                        wuid: 1403891928392,
                        percOpen: 50
                    }],
                    [{
                        exp: 2,
                        open: false,
                        tot: 4,
                        widgetid: "",
                        keywords: [],
                        header: "Oil and Gas",
                        content: "",
                        wuid: 1403891928392,
                        percOpen: 50
                    }]
                ]
            }
        }
    }
}

```