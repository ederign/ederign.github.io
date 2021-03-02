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



### Section 3: Sharing Dependencies Between Apps

#### Using Shared Modules

Both cart and products modules both have faker as a dependency. The bad part is that we are loading in twice. (check vendors-node_modules_faker)

[![Shared](/assets/2021/wiki/shared1.png "Process")](/assets/2021/wiki/shared1.png)

Container should load just one and provide a copy for it. How?

Add to both cart and products webpack.config.js:

```
new ModuleFederationPlugin({
      name: "products",
      filename: "remoteEntry.js",
      shared: ["faker"], <=========
      exposes: {
        "./ProductsIndex": "./src/index",
      },
    }),
```

And then, we just have one faker loaded:

[![Shared](/assets/2021/wiki/shared2.png "Shared")](/assets/2021/wiki/shared2.png)

#### Async Script Loading

After this, we need to add async script loading to our services. If we got this error message:

[![Shared](/assets/2021/wiki/shared3.png "Shared")](/assets/2021/wiki/shared3.png)

We should do this change on our apps:

Move the code to another file, and load it on index like this:


[![Shared](/assets/2021/wiki/shared4.png "Shared")](/assets/2021/wiki/shared4.png)


This step introduces some asynchronicity for loading js code and gives room to webpack the opportunity to figure out which file needs to run successfully. 

Asynd loading respects versioning of our apps. Two different versions makes two lib loadings. You can declare your libs as singleton in order to guarantee that is just a single version of the same app:

```
new ModuleFederationPlugin({
      name: "products",
      filename: "remoteEntry.js",
      shared: {
        faker: {
          singleton: true,
        },
      },
      exposes: {
        "./ProductsIndex": "./src/index",
      },
    }),
```

How to run my code in isolation (microfront end dev) and production? An example:

microfront-end:
```
import faker from "faker";

const mount = (el) => {
  const cartText = `<div> You have ${faker.random.number()} items in your cart</div>`;
  el.innerHTML = cartText;
  //ReactDOM.render(<App />, el) <- if it's react
};

//development mode of products microfrontend
if (process.env.NODE_ENV === "development") {
  const devDiv = document.getElementById("dev-cart");
  if (devDiv) {
    mount(devDiv);
  }
}

export { mount };
```

On container app:

```
import { mount as mountProduct } from "products/ProductsIndex";
import { mount as mountCart } from "cart/CartShow";

console.log("Container");
mountProduct(document.getElementById("my-products"));
mountCart(document.getElementById("my-cart"));
```


### Section 4: Linking Multiple Apps Together

inflx. requid1 : no shared state:  redux, no reducer, rno context, nothing like that between child projects


inflexible 3
css should be scoped
