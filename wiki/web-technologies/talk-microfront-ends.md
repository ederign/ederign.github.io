---
layout: wiki
title: Resumindo 18 meses de adoção de Micro frontend em 30 minutos
last_updated: 2021-03-09
---

### pt-br summary

Nesta palestra, Eder e Alex apresentarão sua visão sobre Arquitetura de Micro frontend, desafios relacionados a  implementação deste paradigma e lições aprendidas na experiência de migração de um monolito de centenas de milhares de linhas de código, desenvolvido por 30+ desenvolvedores distribuídos em 6 diferentes times para micro front-ends.
Serão discutidos exemplos e opções de implementação, BFFs, serviços sync e async, event bus, federated modules e opções para desacoplamento da sua arquitetura de front-end.
Além disto, apresentaremos como foi possível levar o mesmo 'micro front-end' para diversos meios como Web, Desktop, VSCode e Chrome Extension sem nenhuma mudança no código fonte.


Online Editor container application

https://www.thoughtworks.com/radar/techniques/micro-frontend-anarchy

another problems on this post: https://medium.com/swlh/problems-with-micro-frontends-8a8fc32a7d58



### links

#### Micro Frontends
https://martinfowler.com/articles/micro-frontends.html

Good frontend architecture is hard. Scaling frontend development so that many teams can work simultaneously on a large and complex product is even harder.


smaller, more cohesive and maintainable codebases
more scalable organisations with decoupled, autonomous teams
the ability to upgrade, update, or even rewrite parts of the frontend in a more incremental fashion than was previously possible


##### Benefits

- Incremental upgrades
- Simple, decoupled codebases
- Independent deployment

[![Sample Application](/assets/2021/wiki/deployment-micro.png "Sample Application")](/assets/2021/wiki/deployment-micro.png)

- Autonomous teams
[![Sample Application](/assets/2021/wiki/horizontal.png "Sample Application")](/assets/2021/wiki/horizontal.png)

##### Integration approaches

- Server-side template composition
- Build-time integration
```
{
  "name": "@feed-me/container",
  "version": "1.0.0",
  "description": "A food delivery web app",
  "dependencies": {
    "@feed-me/browse-restaurants": "^1.2.3",
    "@feed-me/order-food": "^4.5.6",
    "@feed-me/user-profile": "^7.8.9"
  }
}
```
However, this approach means that we have to re-compile and release every single micro frontend in order to release a change to any individual part of the product


##### Run-time integration via iframes

We often see a lot of reluctance to choose iframes. While some of that reluctance does seem to be driven by a gut feel that iframes are a bit “yuck”, there are some good reasons that people avoid them. The easy isolation mentioned above does tend to make them less flexible than other options. It can be difficult to build integrations between different parts of the application, so they make routing, history, and deep-linking more complicated, and they present some extra challenges to making your page fully responsive.


##### Run-time integration via JavaScript

```
<head>
    <title>Feed me!</title>
  </head>
  <body>
    <h1>Welcome to Feed me!</h1>

    <!-- These scripts don't render anything immediately -->
    <!-- Instead they attach entry-point functions to `window` -->
    <script src="https://browse.example.com/bundle.js"></script>
    <script src="https://order.example.com/bundle.js"></script>
    <script src="https://profile.example.com/bundle.js"></script>

    <div id="micro-frontend-root"></div>

    <script type="text/javascript">
      // These global functions are attached to window by the above scripts
      const microFrontendsByRoute = {
        '/': window.renderBrowseRestaurants,
        '/order-food': window.renderOrderFood,
        '/user-profile': window.renderUserProfile,
      };
      const renderFunction = microFrontendsByRoute[window.location.pathname];

      // Having determined the entry-point function, we now call it,
      // giving it the ID of the element where it should render itself
      renderFunction('micro-frontend-root');
    </script>
  </body>
</html>
```

The above is obviously a primitive example, but it demonstrates the basic technique. Unlike with build-time integration, we can deploy each of the bundle.js files independently. And unlike with iframes, we have full flexibility to build integrations between our micro frontends however we like. We could extend the above code in many ways, for example to only download each JavaScript bundle as needed, or to pass data in and out when rendering a micro frontend.

The flexibility of this approach, combined with the independent deployability, makes it our default choice, and the one that we've seen in the wild most often. We'll explore it in more detail when we get into the full example.

##### Run-time integration via Web Components



#### Styling
A newer approach is to apply all styles programatically with CSS modules or one of the various CSS-in-JS libraries, which ensures that styles are directly applied only in the places the developer intends. Or for a more platform-based approach, shadow DOM also offers style isol

#### Backend communication

- Autonomous teams
[![Sample Application](/assets/2021/wiki/bff-m.png "Sample Application")](/assets/2021/wiki/bff-m.png)


#### Downsides

##### Payload size
ne approach is to externalise common dependencies from our compiled bundles, as we described for the demo application. As soon as we go down this path though, we've re-introduced some build-time coupling to our micro frontends. Now there is an implicit contract between them which says, “we all must use these exact versions of these dependencies”. If there is a breaking change in a dependency, we might end up needing a big coordinated upgrade effort and a one-off lockstep release event. This is everything we were trying to avoid with micro frontends in the first place!
This inherent tension is a difficult one, but it's not all bad news. Firstly, even if we choose to do nothing about duplicate dependencies, it's possible that each individual page will still load faster than if we had built a single monolithic frontend. The reason is that by compiling each page independently, we have effectively implemented our own form of code splitting. In classic monoliths, when any page in the application is loaded, we often download the source code and dependencies of every page all at once. By building independently, any single page-load will only download the source and dependencies of that page. This may result in faster initial page-loads, but slower subsequent navigation as users are forced to re-download the same dependencies on each page. If we are disciplined in not bloating our micro frontends with unnecessary dependencies, or if we know that users generally stick to just one or two pages within the application, we may well achieve a net gain in performance terms, even with duplicated dependencies.

There are lots of “may’s” and “possibly’s” in the previous paragraph, which highlights the fact that every application will always have its own unique performance characteristics. If you want to know for sure what the performance impacts will be of a particular change, there is no substitute for taking real-world measurements, ideally in production. We've seen teams agonise over a few extra kilobytes of JavaScript, only to go and download many megabytes of high-resolution images, or run expensive queries against a very slow database. So while it's important to consider the performance impacts of every architectural decision, be sure that you know where the real bottlenecks are.

Environment 

Operational and governance complexity
- Do you have enough automation in place to feasibly provision and manage the additional required infrastructure?
- Will your frontend development, testing, and release processes scale to many applications?
- Are you comfortable with decisions around tooling and development practices becoming more decentralised and less controllable?
- How will you ensure a minimum level of quality, consistency, or governance across your many independent frontend codebases?