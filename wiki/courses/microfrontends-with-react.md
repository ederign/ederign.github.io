---
layout: wiki
title: Microfrontends with React
last_updated: 2021-02-09
---
Author: Stephen Grider [udemy](https://www.udemy.com/course/microfrontend-course/)

Code lives [here](https://github.com/ederign/experiments/tree/master/federated_modules_lab0)

### Section 1: The Basics of Microfrontends

What are micro frontends?

- Divide a monolithic app into multiple, smaller apps
- Each smaller app is responsible for a distinct feature of the product

Why use them?

- Multiple engineering teams can work on isolation;
- Each smaller app is easier to understand and make changes to;

Ideally, a MFE should not talk between each other, but with some sort of backend API

[![Sample Application](/assets/2021/wiki/mf1.png "Sample Application")](/assets/2021/wiki/mf1.png)

Types of integration

- *Build-Time integration* (compile-time integration): Before the container gets loaded in the browser, it gets access to ProductsList source code;
  - Pros: Easy to setup and understand
  - Cons: Container has to be re-deployed every time ProductsList has updated and tempting to tightly couple Container + ProductsList together;

[![Buiild-Time](/assets/2021/wiki/mf2.png "Build time")](/assets/2021/wiki/mf2.png)

- *Run-Time integration* (client-side integration): After the container gets loaded in the browser, it gets access to ProductsList source code;

  - Pros: ProductsList can be deployed independently at any time and can deploy different versions of ProductsList, and Container can decide which one to use
  - Cons: tooling + setup is far more complicated
  - Example of this integration is Webpack Module Federation
    - most flexible and performant solution around right now
  - [![Run-Time](/assets/2021/wiki/mf3.png "Run time")](/assets/2021/wiki/mf3.png)
- *Server Integration*: while sending down JS to load up Container, a server decides on whether or not to include ProductsList source

Webpack combines many js files (from project and dependencies) into one single file.

### Section 2: The Basics of Module Federation

Steps:

[![Steps](/assets/2021/wiki/mf4.png "Steps")](/assets/2021/wiki/mf4.png)

Host: Container, Remote: Products

#### What module federation does on products project?

[![Federation Products](/assets/2021/wiki/mf5.png "Federation Projects")](/assets/2021/wiki/mf5.png) 

#### What module federation does on container project?

[![Federation Container](/assets/2021/wiki/mf6.png "Federation Container")](/assets/2021/wiki/mf6.png)

#### What is the flow of execution?

[![Federation Flow](/assets/2021/wiki/mf7.png "Federation Container")](/assets/2021/wiki/mf7.png)

#### Configuration options

Container(Host):

[![Container configuration](/assets/2021/wiki/mf8.png "Container Configuration")](/assets/2021/wiki/mf8.png)


Products(Remote):

[![Products configuration](/assets/2021/wiki/mf9.png "Products Configuration")](/assets/2021/wiki/mf9.png)

#### The Development Process

[![Process](/assets/2021/wiki/mf10.png "Process")](/assets/2021/wiki/mf10.png)

index.html of Products and cart are only used during developments of subprojects.

index.html of Container is used during development + production
