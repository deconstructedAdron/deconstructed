---
title: "High Level Architecture"
author: adron-hall
date: 2014-02-16
template: article.jade
---

At a high level the Deconstructed Platform sits across a multi-region, multi-tier architecture that is setup to auto-scale compute, storage and other resources as needed. On the back end the platform uses a comobination of storage mechanisms that are also distributed, storing key value, graph and event series data. Currently these are the key storage types that provide the [consociation](/articles/consociation/) [(definition of consociation)](http://www.merriam-webster.com/dictionary/consociation).

<span class="more"></span>
---



<img src="data-structures.svg" width="100%" height="100%"></img>

<img src="storgie-simple-architecture.svg" width="100%" height="100%"></img>

<img src="storgie-flow.svg" width="100%" height="100%"></img>