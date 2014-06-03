---
title: "Deconstructed Consociated Data"
author: adron-hall
date: 2014-06-02
template: article.jade
---

<h2 id="device">Reading Device Data</h2>

URI: [api.deconstructed.io/device/by](#)

Issuing an HTTP POST against this route and including a body (-d with a curl command) of JSON parameters will return the device or devices that match the criteria passed in. The passed in data can be either deviceid or knownid but not both. Examples of curling this path include:

    curl -u username:password -X POST -H "Content-Type: application/json" -d '**' http://api.deconstructed.io/device/by

Where the data (** above) is passed (via -d with a curl command) the following would be passed based on what type of information will be used to find data by. There are several ways to pass data to get device data by, currenlty this includes:

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

<h2 id="identity">Reading Identity Data</h2>

URI: [api.deconstructed.io/identity/by](#)

This API route provides a query interface very similar to the device by search query interface except that it has an additional parameter option (identitykey) provides only a single element in response for any of the keys. As it returns the data for the device in a post consociated state after a convergence of the data has occurred. The converged by end point provides information

    curl -u username:password -X POST -H "Content-Type: application/json" -d '' http://api.deconstructed.io/identity/by

Where the data is passed (via -d with a curl command) the following would be passed based on what type of information will be used to find data by. There are several ways to pass data to get device data by, currenlty this includes:

 * identitykey: This is the ID that the system uses to track and find the profile records association to an individual device in the system.
```javascript
{"identitykey":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
```
 * devicekey: This is the ID that the system uses to track individual devices and can be used to find an identity by since the identitykey goes along with converged data when it is graphed together to form a complete identity.
```javascript
{"devicekey":"06e5140d-fa4e-4758-8d9d-e707bd19880d"}
```
 * knownid: This can be one or more IDs associated to the IDs tracked against devices.
```javascript
{"knownid":"{"ID":"c625e601-fb42-40f8-a101-33301d290596","emailId":"foo@bar.com"}"}
```
In return a result might look like this:

```javascript
{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"knownid" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}
```

If other profile device information has been added to this device through convergence in identity the data could have a number of other known IDs and related metadata.
