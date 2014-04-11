---
title: "Inbound and Outbound Data"
author: adron-hall
date: 2014-02-17
template: article.jade
---

The Deconstructed Graph Engine automatically graphs relationships between users and devices based on shared user identity values.  A user identity value in Deconstructed is called a “knownid”.  The Engine processes in-bound data in real-time and updates the graph continuously. Devices sharing a “knownid” are associated together in the graph.
When requesting data from the graph, there two domains of data: device-level and user-level (or identity-level).  Device profiles within the graph contain all of the knownid’s collected from that device.  User profiles, or “Identities” contain all of the knownid’s for that user across all of their devices, as well as all of the devices associated with that user.
The purpose of the schema is to provide an outline of how to structure data to send to the Deconstructed Graph Engine for processing.

<span class="more"></span>

* * *

##Overview & Philosophy

The idea behind the Inbound Data Schema isn’t to confine what might be sent to, stored and processed. Instead this is set as a guideline of what will be processed. These specific JSON key value pairs are values that will be acted upon once received by the Graph Engine.

The philosophy is to use the recursive, open ended nature of of JavaScript Object Notation, or JSON as an intelligent storage mechanism for data that is sent to the Deconstructed system. By doing so we gain the use of JavaScript and the native readability that JavaScript has for JSON but also the mass adoption of JSON across many platforms.

### Sending Inbound Data to Deconstructed

At the most basic level there are several required pieces of data. This required data is to ensure that any possible 100% matches between devices can be pulled together into an identity. If these value pairs are left out of the JSON data that is sent to Deconstructed the identifiers and other  data will not be processed for the particular collection. At the root level there are two elements that must be present. These elements; key and value, are shown below.

```javascript
{
    "key" : "a725e312-fb51-49f8-a101-33301d290236",
    "value" : {
    	...all content values go here...
    }
}
```

When referred to in other documentation, the two domains of identity, device or other elements have a key, each are referred to as *identity key* or *device key*.

Also in the value there should be certain elements, many are optional. One of the most important, to draw on the functionality of the Deconstructed services, is a pair with a key of *knownid* and the value of that pair being a list of JSON data pairs that signify keys. This data will be cross-correlated against for known identified matches. Here is an example of the baeline JSON with values that one could submit for *knownid*.

```javascript
{
    "key" : "a725e312-fb51-49f8-a101-33301d290236",
    "value" : {
    	"knownid":{
    		"ID":"c625e601-fb42-40f8-a101-33301d290596",
			"email-md5-hash":"8d86e026da849d333a518a394bc37e0d",
			"secret-id-hash":"1dce4e2a445350c5583d4663f9299af3",
			"twitter-id":"adron",
			"dropbox-hash":"d0c14f38429d9494a96211d660f6a48c",
			"github-id":"adron"
    	}
    }
}
```

...or...

```javascript
{
    "key" : "a3c86502-8d19-4bfb-9922-25f9ed26cda8",
    "value" : {
    	"knownid":{
    		"id":"7aa1ec01-59a9-4185-a990-38e650b0aebb",
			"secret-id-guid":"4499c77d-6db0-4dd7-b516-b4be0aad49a4",
			"dropbox-hash":"d0c14f38429d9494a96211d660f6a48c",
			"github-id":"adron"
    	}
    }
}
```

#### Sending Inbound Metadata Store Metadata to Desconstructed
When sending data to the Deconstructed API additional metadata can be sent along with the standard pieces of data. Some elements in that metadata are stored and utilized in a specific way. In the sections below some examples of adding metadata to the inbound data are shown.
##### User Data Store
One example of metadata that has specific uses, kind of like reserved words in programming languages, is the User Data Store metadata. Here's a complete example with the standard key and knownid values included.

```javascript
{
    "key" : "a725e312-fb51-49f8-a101-33301d290236",
    "value" : {
    	"knownid":{
    		"ID":"c625e601-fb42-40f8-a101-33301d290596",
			"email-md5-hash":"8d86e026da849d333a518a394bc37e0d",
			"secret-id-hash":"1dce4e2a445350c5583d4663f9299af3",
			"twitter-id":"adron",
			"dropbox-hash":"d0c14f38429d9494a96211d660f6a48c7c4",
			"github-id":"adron"
    	}
    	"ms":{
    		"favCoffeeShopGeoJson":{
			  "type": "Feature",
			  "geometry": {
			    "type": "Point",
			    "coordinates": [124.1, 10.4]
			  },
			  "properties": {
			    "name": "Favorite Coffee Shop"
			  }
			},
    		"homeLocationGeoJson":{
			  "type": "Feature",
			  "geometry": {
			    "type": "Point",
			    "coordinates": [125.6, 10.2]
			  },
			  "properties": {
			    "name": "Home"
			  }
			},
    		"officeLocationGeoJson":{
			  "type": "Feature",
			  "geometry": {
			    "type": "Point",
			    "coordinates": [125.3, 10.3]
			  },
			  "properties": {
			    "name": "Office"
			  }
			},
			"favoriteDevice":"iPad",
			"mostUsedDevice":"IBM Work Laptop",
			"session":{
    		  "session-device":"iPhone"
    		  "a29bc541-d8d2-4b16-871e-b09357d6121ba9c13dfd-e359-4e5b-9cd8-66c3f13fb7c4"
    		  "session-device":"Android Tablet"
    		  "a29bc541-d8d2-4b16-871e-b09357d6121ba9c13dfd-e359-4e5b-9cd8-66c3f13fb7c4"
    		  "session-device":"Android Samsung S3"
    		  "a29bc541-d8d2-4b16-871e-b09357d6121ba9c13dfd-e359-4e5b-9cd8-66c3f13fb7c4"
    		  "session-device":"Android Samsung S3"
    		  "a29bc541-d8d2-4b16-871e-b09357d6121ba9c13dfd-e359-4e5b-9cd8-66c3f13fb7c4"
    		}
    	}
    }
}
```
There are several key pieces of Metadata Store information above. The first three elements are what is called [Geo JSON](http://geojson.org/). Some great examples of displaying the GeoJSON Data is using [Leaflet.js](http://leafletjs.com/). The 4th and 5th elements; favoriteDevice and mostUsedDevice are standard string data representing device use of the user.