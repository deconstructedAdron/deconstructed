---
title: "Deconstructed Data Collection"
author: adron-hall
date: 2014-06-02
template: article.jade
---

<h2 id="writing">Writing Data</h2>

The root of all API calls are located at http://api.deconstructed.io/. The following are all listed with the root assumed to be this URI. All paths are then appended to this root. Each API call is accessed via an access token for your particular account. This value is appended to the URI with a parameter variable access_token=123456789.

### /device/

Post to this path to add device specific user identifying data that will be used to identify a new device and user. This is the single end point to send data that will be tracked, managed and processed with the identity engine. For an example of JSON data to pass into the services check out the [Inbound Data Schema](/articles/inbound-data-schema/).

Examples of this path to write a new device and associated data:

    curl -u username:password -X POST -H "Content-Type: application/json" -d '{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"knownid" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}' http://api.deconstructed.io/device

Example results would look like this, with the key being returned when the write is successful.

```javascript
{"key": "06e5140d-fa4e-4758-8d9d-e707bd19880d"};
```
