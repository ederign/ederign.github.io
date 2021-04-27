---
layout: post
title:  "DashBuilder: an Apache licensed Business reporting and monitoring tool"
permalink: /:year/:month/:day/:title:output_ext
date:   2021-04-27 00:00:00 -0500
fav: true
---

DashBuilder is a tool for the building of reporting and monitoring business dashboards, licensed under the business friendly Apache Software License (ASL). It has a strong emphasis on flexible navigation and page layouts, to ensure you can organise your content the way you want. It is decoupled from the data sources, with support for Prometheus, JDBC, Elastic Search, Kafka, CVS and Java Beans. It has a simple JavaScript API for extensions, and provides out of the box support for Victory Charts and Apex Charts - with the later providing time series support.

[![Dashbuilder](/assets/2021/dbblog0.gif "Dashbuilder")](/assets/2021/dbblog0.gif)

The website is very out of date, but we are in the process of revamping, which will be done in time for our next big DashBuilder release. Our main priority right now is migration to [Quarkus](https://quarkus.io/) to get a more cloud native experience and to develop more getting started guides. We also plan to revisit our JavaScript API for extensions, with possible integration with GrapeJS which has a really nice JavaScript API for what it calls Blocks. We also have ongoing work to provide a more generalized way for how we extend the UI for data sources. We are also integrating Dashboard components and pages with Multiplying Architecture (the technology behind [Kogito Tooling](https://kogito.kie.org/)).

We hope to have the improved getting started guides available in a few weeks, the Quarkus port within 2 months, so stay tuned on our blog for [updates](http://blog.kie.org/)!

Below is an overview of the more interesting features and work streams for DashBuilder, along with links to posts with more details for each topic.

## Flexible Layout and Navigation

One of the key features of Dashbuilder is that it allows you to compose full-feature business dashboards in a drag and drop way. You can combine a whole mix of components in your Dashboard Page, including reporting components (Bar, Pie, Line, etc.), HTML components, custom extensions, and even other Dashboard Pages (full recursive!).


[![Dashbuilder](/assets/2021/dbblog1.gif "Dashbuilder")](/assets/2021/dbblog1.gif)

After creating your pages, Dashbuilder also lets you create versatile navigation trees, allowing you to display your pages as application menu items or components like tiles, tree, and carousel.

[![Dashbuilder](/assets/2021/dbblog2.gif "Dashbuilder")](/assets/2021/dbblog2.gif)

## Prometheus, Kafka, Elastic Search, Kafka, Elastic Search, CSV and JDBC Support

Dashbuilder can extract data from heterogeneous sources of information such as  Prometheus, JDBC, Elastic Search, Kafka, CVS, and Java Beans. This raw data can be later grouped, filtered, transposed, and personalized and then used as input for each component. 

[![Dashbuilder](/assets/2021/dbblog3.gif "Dashbuilder")](/assets/2021/dbblog3.gif)

For additional information, take a look at this post with a deep dive in our [Prometheus](https://blog.kie.org/2021/03/building-prometheus-dashboards-in-business-central.html) support.

## Victory Charts and Other Components

It is possible to use any data visualization library you want in DashBuilder using External Components. Use external components to either add new ways to visualize data like [heatmaps](https://blog.kie.org/2021/01/heatmap-component-for-business-central-and-jbpm.html) or use alternative libraries such as [Victory Chars](https://www.patternfly.org/v4/charts/about/).

Dashboard with Custom components:

[![Dashbuilder](/assets/2021/dbblog4.gif "Dashbuilder")](/assets/2021/dbblog4.gif)

Victory Chart Custom components:

[![Dashbuilder](/assets/2021/dbblog5.png "Dashbuilder")](/assets/2021/dbblog5.png)

## Time Series with Apex Charts

We also recently introduced a new component based on Apex Charts to represent time-series metrics to smoothly support the new Prometheus data set provider.

[![Dashbuilder](/assets/2021/dbblog6.gif "Dashbuilder")](/assets/2021/dbblog6.gif)

Now, you can provide a custom data set or Prometheus metrics and create visualizations of your time series data on a line or area chart using DashBuilder. See this [blog post](https://blog.kie.org/2021/03/time-series-component-for-dashbuilder.html) for more details.

## DashBuilder Lightweight Runtime and Multi-Tenancy

The traditional DashBuilder web application has the capability to author and run your Dashboards.
In order to expand our set of use cases and also target containerized environments, we recently released DashBuilder Runtimes, a lightweight application able to run dashboards with a lower footprint.

DashBuilder Runtimes can operate in two different modes. The first one, Static, focused on immutable images and able to display one dashboard per installation. The second, Multi-Mode, can run in a multi-tenancy model, allowing you to have multiple dashboards in the same installation.

[![Dashbuilder](/assets/2021/dbblog7.gif "Dashbuilder")](/assets/2021/dbblog7.gif)

For more details, check out the announcement of [DashBuilder Runtime](https://blog.kie.org/2020/09/introducing-dashbuilder-runtime.html) and our [multi tenancy](https://blog.kie.org/2020/09/multi-dashboards-support-in-dashbuilder-runtime.html) mode.

## Easy way to import/export your dashboards

Ok, but how can I move Dashboards from authoring to runtime?
It's super easy! Using our Import/Export tool, you can export a specific page or a set of pages along with its datasets to run it on DashBuilder Runtime!

[![Dashbuilder](/assets/2021/dbblog8.gif "Dashbuilder")](/assets/2021/dbblog8.gif)

For more details, check out this [blog post](https://blog.kie.org/2020/09/gradual-export-dashboards-from-business-central.html).

## Embedded Mode

With embedded mode, DashBuilder Runtime can be part of users’ applications. Every page of yours can be accessed via a specific URL. 

We also provide a nice REST API that allows you to query the Runtime for details of existing dashboards and upload new ones directly.

[![Dashbuilder](/assets/2021/dbblog9.gif "Dashbuilder")](/assets/2021/dbblog9.gif)

For more details, check out this [blog post](https://blog.kie.org/2020/09/dashbuilder-runtime-embedded-mode.html).

## JavaScript API for Extensions

But how to write an extension with my own component? You develop them using our public Javascript API. This API helps you consume data from DashBuilder, and you can use any Javascript libraries to build your visualizations.

Along with this API, it is also possible to develop your component using a component dev package, which emulates Business Central and sends configurable data sets and configuration to the component.

[![Dashbuilder](/assets/2021/dbblog10.gif "Dashbuilder")](/assets/2021/dbblog10.gif)

For more information, please check this [blog post](https://blog.kie.org/2021/02/dashbuilder-external-components-javascript-api-2.html).

## Declarative Programmatic API

Using the Declarative Programmatic API,  you can create their Dashboards, pages, components, and data sets directly on Java. Here is an example of the usage of such API:

<script src="https://gist.github.com/ederign/3f1967f21cb3e419cfb6a92f4291daca.js"></script>

It will generate the following dashboard:

[![Dashbuilder](/assets/2021/dbapi.png "Dashbuilder")](/assets/2021/dbapi.png)

We also have a “dev mode” connected to a DashBuilder Runtime, which automatically updates the DashBuilder Runtime while developing and exporting the dashboard.

[![Dashbuilder](/assets/2021/dbapi1.gif "Dashbuilder")](/assets/2021/dbapi1.gif)

## How to start?

The best point to start with DashBuilder is following this [blog post](https://blog.kie.org/2020/10/dashbuilder-runtime-demos.html). You can also look at our demos on this [repository](https://github.com/jesuino/dashbuilder-docker/tree/master/demos), where we provide some Docker images ready to use.
Feel free to use the comment section here to ask any further comment!

 Thanks for reading!

[kie]