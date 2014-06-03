---
title: "API Docs - Devices By"
author: adron-hall
date: 2014-06-02
template: article.jade
---

### /device/by

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