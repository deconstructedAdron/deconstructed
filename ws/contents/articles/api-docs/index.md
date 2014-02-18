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
    *   [Philosophy](#philosophy)
    *   [Documentation Conventions](#conventions)
*   [Identity API Services](#consociation)
*   [Consociation API Services](#identity)

* * *

<h2 id="overview">Overview</h2>

<h3 id="philosophy">Philosophy</h3>

The idea behind the API services is to provide a simple RESTful style interface for interaction with client mobile apps, native interfaces, browser based clients or whatever might make use of this data consociation.

<h3 id="conventions">Documentation Conventions</h3>

In this documentation many of the API calls will have examples provided in JavaScript initially and over time in other prospective languages such as Csharp, Java, Objective-C and others.

#### Example JavaScript Code

```javascript
function getStorgieConsociationData() {
    return StorgieStuff;
}
```

#### ObjectiveC

```objectivec
#import <stdio.h>

int main(void)
{
    printf("Hello, Storgie!\n");
    return 0;
}
```

#### Example CSharp Code

```cs
class StorgieGetter
{
    static void Main()
    {
        System.Console.WriteLine(Consociation.Data.StorgieStuff());
    }
}
```

#### Java

```java
public class StorgieGetter {
   public static void main(String[] args) {
       System.out.println(Storgie.Data.StorgieStuff());
   }
}
```

<h2 id="identity">Identity</h2>

The root of all API calls are located at http://api.deconstructed.io/. The following are all listed with the root assumed to be this URI. All paths are then appended to this root.

### /api/

Submit a get against this path for a status on the Deconstructed Ecosystem. This API end point will return a number of values relevant to determine system availability and status.

Example of calling this path with cURL:

    curl api.deconstructed.io/api

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

### /ident/

Post to this path to add any new application event that can be used to identify a new device and user. This is the single end point to send data that will be tracked, managed and processed with the consociation engine. For an example of JSON data to pass into the ident service check out the [Inbound Consociated Data Schema](/articles/inbound-data-schema/).

Examples of this path include:

    curl -X POST -H "Content-Type: application/json" -d '{"key":"06e5140d-fa4e-4758-8d9d-e707bd19880d", "value":{"KnownID" : {"ID" : "c625e601-fb42-40f8-a101-33301d290596"}}}' http://api.deconstructed.io/ident/

Example results would look like this, with the key being returned when the write is successful.

```javascript
{"key": "06e5140d-fa4e-4758-8d9d-e707bd19880d"};
```

### /ident/:id

Get against this path to pull any ident information by the id passed in as a parameter. Examples of this path include:

    http://api.deconstructed.io/ident/1

or

    http://api.deconstructed.io/ident/h4sh4y0u

or

    http://api.deconstructed.io/ident/1234-big1-guid-goes43here12


Example results would look like:

```javascript
{“”:”"}
```

<h2 id="consociation">Consociation</h2>

### /convergence/

### /converged/

### /converged/:id

### /converged/:query