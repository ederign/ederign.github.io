---
layout: post
title:  "Design Tools Highlights on Kogito and Business Central, April 2021"
permalink: /:year/:month/:day/:title:output_ext
date:   2021-04-08 00:00:00 -0500
fav: true
---

In the last months, the Design Tools Team released many cool new features on [Kogito Tooling 0.9.0](https://github.com/kiegroup/kogito-tooling/releases) and [Business Central 7.52.0](https://www.jbpm.org/). This post will do a quick overview of those. I hope you enjoy it!

### Dashbuilder Programmatic Layout API

Until the launch of this new API, the only way to create dashboards on Dashbuilder was via drag and drop on Layout Editor. Now, users can create their Dashboards, pages, components, and data sets directly on Java. 

Here is an example of the usage of such API:

<script src="https://gist.github.com/ederign/3f1967f21cb3e419cfb6a92f4291daca.js"></script>

It will generate the following dashboard:


[![Dashbuilder](/assets/2021/dbapi.png "Dashbuilder")](/assets/2021/dbapi.png)

We also introduced a "dev mode" to Dashbuilder Runtime, which automatically updates the Dashbuilder Runtime while developing and exporting the ZIP.  Soon, we will publish a blog post with more details about this new feature, but meanwhile, a sneak peek of authoring workflow using it:


[![Dashbuilder](/assets/2021/dbapi1.gif "Dashbuilder")](/assets/2021/dbapi1.gif)


### DMN Editor - Enhanced code-completion for Literal FEEL expressions

Context-aware code completion is one of the most important features an IDE can provide to speed up coding, reduce typos and avoid other common mistakes. On Kogito Tooling 0.9.0 release, we introduced enhanced code-completion for Literal FEEL expressions. 

Check out this video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/VXENjnEbwO8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

See this full [blog post](https://blog.kie.org/2021/03/how-the-new-feel-code-completion-works-under-the-hoods.html) for details.

### BPMN Editor - Read-Only mode

Since October, we also ship our editors as a standalone npm package. One of my favorite features of the standalone is the read-only mode because it is really useful for diagram visualization.  Now, this mode is also supported on BPMN.
The read-only mode is also used for the visualization of diagrams on our Chrome Extension.

[![BPMN](/assets/2021/bpmn.gif "BPMN")](/assets/2021/bpmn.gif)

### Work Item Definition support improvements

To evolve our Work Item Definition support on Kogito Tooling BPMN editor, we included on 0.9.0 a lot of improvements in this area, primarily related to a better parsing mechanism and also better compatibility with Business Central. Now, we also search for wids and icons the 'global' directory used on BC.


[![BPMN](/assets/2021/bpmn.png "BPMN")](/assets/2021/bpmn.png)

### Dashbuilder Prometheus Data Set Provider

Dashbuilder can read data from multiple types of data set sources, including CSV, SQL, ElasticSearch, and Kie Server. Since Business central 7.50.0 Final, we introduced a new type of provider for data sets: Prometheus.


[![DB Prometheus](/assets/2021/dbpr.png "DB Prometheus")](/assets/2021/dbpr.png)

Prometheus is the standard for collecting metrics. It has connectors to very well-known systems, such as Kafka and metrics can be easily consumed from third-party systems. Furthermore, Kie Server by default also exports [Prometheus metrics](https://blog.kie.org/2019/06/jbpm-monitoring-using-prometheus-and-grafana.html)! See a sample Dashboard based on Prometheus data:

[![DB Prometheus](/assets/2021/dbpr1.png "DB Prometheus")](/assets/2021/dbpr1.png)

For a full description of this new feature, take a look at this [blog post](https://blog.kie.org/2021/03/building-prometheus-dashboards-in-business-central.html).

### Dashbuilder Kafka Data Set Provider

We also recently introduced Dashbuilder support for Kafka data sets. Kafka is the standard event streaming platform for cloud applications and RHPAM/Kogito systems expose metrics using Kafka, so this is the reason why we added Kafka support on Dashbuilder as a data set provider.


[![DB Kafka](/assets/2021/ka.gif "DB Kafka")](/assets/2021/ka.gif)

Soon we will publish a blog post with more details about this new feature.

### Dashbuilder Time Series Displayer

This new component represents time-series metrics to smoothly support the new Prometheus data-set provider.


[![DB time](/assets/2021/time_series.gif "DB time")](/assets/2021/time_series.gif)

Now, you can provide a custom dataset or Prometheus metrics and create visualizations of your time series data on a line or area chart using Dashbuilder. See this [blog post](https://blog.kie.org/2021/03/time-series-component-for-dashbuilder.html) for more details.

### GWT 2.9 and JDK11 upgrade

After a collective effort involving many people from a lot of different teams, we also did two major upgrades on our codebase, supporting JDK11 compilation and GWT 2.9 on Business Central. This is a huge effort in a sizable codebase, so congrats to everyone involved! 

### Other important issues and improvements:

#### BPMN:

* [KOGITO-3853](https://issues.redhat.com/browse/KOGITO-3853) Move the structure option to the top of the Data Type drop-down
* [JBPM-9597](https://issues.redhat.com/browse/JBPM-9597) - [BPMN] Open subprocesses in a new editor on BC only
* [RHPAM-3207](https://issues.redhat.com/browse/RHPAM-3207) Stunner - Text area for scripts is cropped/shifted
* [RHPAM-3250](https://issues.redhat.com/browse/RHPAM-3250) Stunner - Not all illegal characters are removed from Data Object name
* [KOGITO-3528](https://issues.redhat.com/browse/KOGITO-3528): Erase of WID 'nodes' types 

#### DMN:

* [KOGITO-3853](https://issues.redhat.com/browse/KOGITO-3853) Move the structure option to the top of the Data Type drop-down
* [DROOLS-6181](https://issues.redhat.com/browse/DROOLS-6181) Allow sorting in guided decision table when clicking the column name

#### SceSim

* [DROOLS-5775](https://issues.redhat.com/browse/DROOLS-5775) Test Scenario does not support nested Enum type attributes
* [DROOLS-6075](https://issues.redhat.com/browse/DROOLS-6075) Scenario Simulation type error popup when constraint applied to DMN data type
* [DROOLS-5876](https://issues.redhat.com/browse/DROOLS-5876) Display actual test results instead of a generic message
* [KOGITO-4190](https://issues.redhat.com/browse/KOGITO-4190) SceSim runner does not display reason for failure

### Thank you to everyone involved!

I would like to thank everyone involved with this release, from the excellent KIE Tooling Engineers to the lifesavers QEs and the UX people that help us look awesome!
