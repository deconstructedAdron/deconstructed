---
title: "Inbound Data Schema"
author: adron-hall
date: 2014-02-17
template: article.jade
---

The Deconstructed Engine processes certain data as the data is collected, in real-time, by client apps and brought into the system. The purpose of the schema is to provide an outline of what is used for processing and adding value to the data that is sent to Deconstructed. This data is then processed for consociation and then provided by various medium.

<span class="more"></span>

* * *


##Overview & Philosophy

The idea behind the Inbound Consociated Data Schema isn't to confine what might be sent to, stored and processed. Instead this is set as a guideline of what will be processed. These specific schema JSON key value pairs are values that will be acted upon once received by the Consociation Engine.

The philosophy is to use the recursive, open ended nature of of JavaScript Object Notation, or JSON as an intelligent storage mechanism for data that is sent to the Deconstructed system. By doing so we gain the use of JavaScript and the native readability that JavaScript has for JSON but also the mass adoption of JSON across many platforms.

### Baseline JSON Data

At the most basic level there are several key required pieces of data. If these value pairs are left out of the JSON data that is sent to Deconstructed the identifiers and other  data will not be processed for the particular collection. At the root level there are two elements that must be present. These elements; key and value, are shown below.

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

Other data can be sent in the value. Here's a few examples that show other data that can be sent along in any addition.

```javascript
{
    "key" : "a3c86502-8d19-4bfb-9922-25f9ed26cda8",
    "value" : {
    	"knownid":{
    		"id":"7aa1ec01-59a9-4185-a990-38e650b0aebb",
			"secret-id-guid":"4499c77d-6db0-4dd7-b516-b4be0aad49a4",
			"dropbox-hash":"d0c14f38429d9494a96211d660f6a48c",
			"github-id":"adron"
    	},
		"company-domain":{
		},
		"delete":"marked",
		"lorum-ipsum-whatev":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent augue dolor, pulvinar quis tortor viverra, pellentesque tristique augue. Curabitur lorem massa, ullamcorper quis nunc id, convallis ultricies nibh. Sed dapibus facilisis feugiat. Etiam porta ullamcorper euismod.",
		"big-money":"432.21",
		"purchase":"864.42",
		"created":"04/10/2018 22:34",
		"last-edit":"05/14/2018 23:17",
		"stamp":"05/15/2018 02:34"
    }
}
```
