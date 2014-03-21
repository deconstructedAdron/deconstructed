---
title: "API Docs"
author: adron-hall
date: 2014-02-15
template: article.jade
---

The Deconstructed APIs are an extremely simple way to manage known identities across devices. Devices are collected via the device services, with the Deconstructed service working in real-time to pull those correlated devices together to form complete identities for management of identity profiles across devices.

<span class="more"></span>

APIs
===

*   [Overview](#overview)
*   [Device API Services](#device)
*   [Identity API Services](#identity)

* * *

<h2 id="overview">Overview</h2>

<h3 id="philosophy">Philosophy</h3>

The idea behind the API services is to provide a simple RESTful style interface for interaction with client mobile apps, native interfaces, browser based clients or whatever might make use of this data identity.

<h2 id="device">device</h2>

The root of all API calls are located at http://api.deconstructed.io/. The following are all listed with the root assumed to be this URI. All paths are then appended to this root. Each API call is accessed via an access token for your particular account. This value is appended to the URI with a parameter variable access_token=123456789.

### /device/

Post to this path to add device specific user identifying data that will be used to identify a new device and user. This is the single end point to send data that will be tracked, managed and processed with the identity engine. For an example of JSON data to pass into the services check out the [Inbound Data Schema](/articles/inbound-data-schema/).

Examples of this path include:

    curl -X POST -H "Content-Type: application/json" -d '{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"knownid" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}' http://api.deconstructed.io/device/?access_token=123456789

Example results would look like this, with the key being returned when the write is successful.

```javascript
{"key": "06e5140d-fa4e-4758-8d9d-e707bd19880d"};
```

### /device/by

Get against this path to pull any device information by the id passed in as a parameter. This can include the deviceid or knownid. Examples of curling this path include:

    curl -X POST -H "Content-Type: application/json" -d '' http://api.deconstructed.io/device/by/?access_token=123456789

Where the data is passed (via -d with a curl command) the following would be passed based on what type of information will be used to find data by. There are several ways to pass data to get device data by, currenlty this includes:

 * deviceid: This is the ID that the system uses to track and find the device records association to a single device in the system.
```javascript
{"deviceid":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
```
 * knownid: This can be one or more IDs associated to the IDs tracked against identities. [Currently unreleased feature]
```javascript
{"knownid":"{"ID":"c625e601-fb42-40f8-a101-33301d290596","emailId":"foo@bar.com"}"}
```

Example results would look like:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"knownid" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```

<h2 id="identity">Identity</h2>

### /identities/

The convergence end point provides rolled up information for the number of convergences that have occurred in the last 5 days. An example of curling this path include:

    curl -X http://api.deconstructed.io/identities/?access_token=123456789

Example results would look like:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"knownid" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```

### /identity/by

This API end point provides a query interface very similar to the device by interface except that it provides only a single response for any of the keys. As it returns the data for the device in a post consociated state after a convergence of the data has occurred. The converged by end point provides information

    curl -X POST -H "Content-Type: application/json" -d '' http://api.deconstructed.io/identity/by/?access_token=123456789

Where the data is passed (via -d with a curl command) the following would be passed based on what type of information will be used to find data by. There are several ways to pass data to get device data by, currenlty this includes:

 * identitykey: This is the ID that the system uses to track and find the profile records association to an individual device in the system.
```javascript
{"identitykey":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
```
 * devicekey: This is the ID that the system uses to track individual devices and can be used to find an identity by since the identitykey goes along with converged data when it is graphed together to form a complete identity.
```javascript
{"devicekey":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
``` 
 * knownid: This can be one or more IDs associated to the IDs tracked against identities. [Currently unreleased feature]
```javascript
{"knownid":"{"ID":"c625e601-fb42-40f8-a101-33301d290596","emailId":"foo@bar.com"}"}
```
In return a result might look like this:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"knownid" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```

If other profile device information has been added to this device through convergence in identity the data could have a number of other known IDs and related metadata.

