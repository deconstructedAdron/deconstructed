---
title: "Inbound Consociated Data Schema"
author: adron-hall
date: 2014-02-17
template: article.jade
---

The [Consociation Engine](/articles/consociation/) processes certain data as the data is collected by client apps and brought into the system. The purpose of the schema is to provide an outline of what is used for processing and adding value to the data that is sent to Deconstructed. This data is then processed for consociation and then provided by various medium.

<span class="more"></span>

* * *


##Overview & Philosophy

The idea behind the Inbound Consociated Data Schema isn't to confine what might be sent to, stored and processed. Instead this is set as a guideline of what will be processed. These specific schema JSON key value pairs are values that will be acted upon once received by the Consociation Engine.

The philosophy is to use the recursive, open ended nature of of JavaScript Object Notation, or JSON as an intelligent storage mechanism for data that is sent to the Deconstructed system. By doing so we gain the use of JavaScript and the native readability that JavaScript has for JSON but also the mass adoption of JSON across many platforms.

### Baseline JSON Data

At the most basic level there are several key required pieces of data. If these value pairs are left out of the JSON data that is sent to Deconstructed the identifiers and other consociated data will not be processed for the particular collection.

In the JSON data there needs to be a pair with a key of "KnownID" and the value is then a list of JSON data pairs that signify what keys this data will be cross-correlated against for known identified matches.
```javascript
{
    "KnownID" : {
        "ID" : "c625e601-fb42-40f8-a101-33301d290596"
    }
}
```
Other key pairs can be added to match across, some examples are provided in the JSON data below. In this example 
```javascript
{
    "KnownID" : {
        "ID" : "c625e601-fb42-40f8-a101-33301d290596"
        "email_hash" : "8743b52063cd84097a65d1633f5c74f5"
        "identifier" : "7674b50e-4085-486a-b6b9-4de75927c551"
        "a_device_hash_id" : "$P$984478476IagS59wHZvyQMArzfx58u."
        "etcid" : "b302cae5-f638-4668-acb1-4e12b3eac170"
    }
}
```