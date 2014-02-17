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
*   [Identity API Services](#identity)
*   [Consociation API Services](#consociation)

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

<h2 id="identity">Identity</h3>



// storgie api identity ident management.
app.get('/api', api.storgie_stat);
app.post('/ident', api.ident_create);
app.get('/ident/:id', api.ident_by_id);


<h2 id="consociation">Consociation</h3>


// storgie api converged data
app.get('/convergence', api.convergence);
app.post('/converged', api.converged_create);
app.get('/converged/:id', api.converged_by_id);
app.get('/converged/:query', api.converged_by_query);
