---
title: "API Docs"
author: adron-hall
date: 2014-02-15
template: article.jade
---

The Deconstructed APIs are an extremely simple way to manage known identities across devices.

<span class="more"></span>

APIs
===

*   [Overview](#overview)
*   [Identity API Services](#identity)
*   [Consociation API Services](#consociation)

* * *

<h2 id="overview">Overview</h2>

<h3 id="philosophy">Philosophy</h3>

The idea behind the API services is to provide a simple RESTful style interface for interaction with client mobile apps, native interfaces, browser based clients or whatever might make use of this data consociation.

<h2 id="identity">Identity</h2>

The root of all API calls are located at http://api.deconstructed.io/. The following are all listed with the root assumed to be this URI. All paths are then appended to this root. Each API call is accessed via an access token for your particular account. This value is appended to the URI with a parameter variable access_token=[123456789].

### /stat/

Submit an HTTP get against this path for a status on the Deconstructed Ecosystem. This API end point will return a number of values relevant to determine system availability and status.

Example of calling this path with cURL:

    curl api.deconstructed.io/stat?access_token=123456789

Example results would look like:

```javascript
{   "Servers":2,
    "Compute":"2% Average Across Servers.",
    "Memory":"2% Average Memory Consumption.",
    "Stat": {
        "Compute":"0 at Peak of 70% utilization.",
        "Memory":"None beyond threshold of 80% Memory utilization.",
        "Stamp":1392750541484 },
    "Stamp":1392750541484 }
```

Identity Tracking & Retrieval

### /identity/

Post to this path to add any new application event that can be used to identify a new device and user. This is the single end point to send data that will be tracked, managed and processed with the consociation engine. For an example of JSON data to pass into the ident service check out the [Inbound Consociated Data Schema](/articles/inbound-data-schema/).

Examples of this path include:

    curl -X POST -H "Content-Type: application/json" -d '{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"KnownID" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}' http://api.deconstructed.io/identity/?access_token=123456789

Example results would look like this, with the key being returned when the write is successful.

```javascript
{"key": "06e5140d-fa4e-4758-8d9d-e707bd19880d"};
```

### /identity/by

Get against this path to pull any ident information by the id passed in as a parameter. Examples of curling this path include:

    curl -X POST -H "Content-Type: application/json" -d '' http://api.deconstructed.io/identity/by/?access_token=123456789

Where the data is passed (via -d) the following would be passed based on what type of information will be used to find data by. There are several ways to pass data to get identity data by, currenlty this includes:

 * Root ID: This is the ID that the system uses to track and find the profile records association to an individual identity in the system.
```javascript
{"rootid":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
```
 * Known ID: This can be one or more IDs associated to the IDs tracked against identities. [Currently unreleased feature]
```javascript
{"knownid":"{"ID":"c625e601-fb42-40f8-a101-33301d290596","emailId":"foo@bar.com"}"}
```
 * search: This is a query based on SOLR/Lucene to find data with. [Currently unreleased feature]
```javascript
{"search":"portland"}
```

Example results would look like:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"KnownID" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```


<h2 id="consociation">Consociation</h2>

### /convergence/

The convergence end point provides rolled up information for the number of convergences that have occurred in the last 5 days. An example of curling this path include:

    curl -X http://api.deconstructed.io/convergence/?access_token=123456789

Example results would look like:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"KnownID" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```

### /converged/by

This API end point provides a query interface very similar to the identity by interface except that it provides only a single response for any of the keys. As it returns the data for the identity in a post consociated state after a convergence of the data has occurred. The converged by end point provides information

    curl -X POST -H "Content-Type: application/json" -d '' http://api.deconstructed.io/converged/by/?access_token=123456789

Where the data is passed (via -d) the following would be passed based on what type of information will be used to find data by. There are several ways to pass data to get identity data by, currenlty this includes:

 * Root ID: This is the ID that the system uses to track and find the profile records association to an individual identity in the system.
```javascript
{"root":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
```
 * Known ID: This can be one or more IDs associated to the IDs tracked against identities. [Currently unreleased feature]
```javascript
{"known":"{"ID":"c625e601-fb42-40f8-a101-33301d290596","emailId":"foo@bar.com"}"}
```
 * search: This is a query based on SOLR/Lucene to find data with. [Currently unreleased feature]
```javascript
{"search":"portland"}
```

In return a result might look like this:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"KnownID" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```

If other profile identity information has been added to this identity through convergence in consociation the data could have a number of other known IDs and related metadata.
