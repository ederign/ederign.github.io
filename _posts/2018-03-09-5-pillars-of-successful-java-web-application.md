---
layout: post
title:  "5 Pillars of a Successful Java Web Application"
permalink: /:year/:month/:day/:title:output_ext
date:   2018-09-02 00:00:00 -0500
fav: true
---
[Alex Porcelli](https://twitter.com/porcelli) and I had the opportunity to present at JavaOne San Francisco 2017 two talks related to our work: [“5 Pillars of a Successful Java Web Application](https://speakerdeck.com/ederign/5-pillars-of-a-successful-java-web-application-1)” and [The Hidden Secret of Java Open Source Projects](https://speakerdeck.com/ederign/the-hidden-secret-of-java-open-source-projects).

[![Java One Audience](/assets/2018/j1audience.jpg "Java One Audience")](/assets/2018/j1audience.jpg)

It was great to share our cumulative experience over the years building the workbench and the web tooling for the Drools and jBPM platform and both talks had great attendance (250+ people in the room).

In this post, we’ll detail our “5 Pillars of a Successful Java Web Application”, trying to give you an overview of our research and a taste of participating in a great event like Java One.

There are a lot of challenges related to building and architecting a web application, especially if you want to keep your codebase updated with modern techniques without throwing away a lot of your code every two years in favor of the latest trendy JS framework.

In our team we are able to successfully keep a 7+ year old Java application up-to-date, combining modern techniques with a legacy codebase of more than 1 million LOC, with an agile, sustainable, and evolutionary web approach.

More than just choosing and applying any web framework as the foundation of our web application, we based our web application architecture on 5 architectural pillars that proved crucial for our platform’s success. Let’s talk about them:

# 1st Pillar: Large Scale Applications

The first pillar is that every web application architecture should be concerned about the potential of becoming a long-lived and mission-critical application, or in other words, a large-scale application.= Even if your web application is not exactly big like ours (1mi+ lines of web code, 150 sub-projects, +7 years old) you should be concerned about the possibility that your small web app will become a big and important codebase for your business. What if your startup becomes an overnight success? What if your enterprise application needs to integrate with several external systems?

Every web application should be built as a large-scale application because it is part of a distributed system and it is hard to anticipate what will happen to your application and company in two to five years.

And for us, a critical tool for building these kinds of distributed and large-scale applications throughout the years has been **static typing**.

## Static Typing

The debate of static vs. dynamic typing is very controversial. People who advocate in favor of dynamic typing usually argue that it makes the developer’s job easier. This is true for certain problems.

However, static typing and a strong type system, among other advantages, simplify identifying errors that can generate failures in production and, especially for large-scale systems, make **refactoring** more effective.

Every application demands constant refactoring and cleaning. It’s a natural need. For large-scale ones, with codebases spread across multiple modules/projects, this task is even more complex. The confidence when refactoring is related to two factors: test coverage and the tooling that only a static type system is able to provide.

For instance, we need a static type system in order to find all usages of a method, in order to extract classes, and most importantly to figure out at **compile time** if we accidentally broke something.

But we are in web development and JavaScript is the language of the web. How can we have static typing in order to refactor effectively in the browser?

# Using a transpiler

A transpiler is a type of compiler that takes the source code of a program written in one programming language as its input and produces equivalent source code in another programming language.

This is a well-known Computer Science problem and there are a [lot](https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js) of transpilers that output JavaScript. In a sense, JavaScript is the assembly of the web: the common ground across all the web ecosystems. We, as engineers, need to figure out what is the best approach to deal with JavaScript’s dynamic nature.

A Java transpiler, for instance, takes the Java code and transpiles it to JavaScript at compile time. So we have all the advantages of a statically-typed language, and its tooling, targeting the browser.

# Java-to-JavaScript Transpilation

The transpiler that we use in our architecture, is GWT. This choice is a bit controversial, especially because the GWT framework was launched in 2006, when the web was a very different place.

But keep in mind that every piece of technology has its own good parts and bad parts. For sure there are some bad parts in GWT (like the Swing Style Widgets, multiple permutations per browser/language), but keep in mind that for our architecture what we are trying to achieve is static typing on the web, and for this purpose the GWT compiler is **amazing**.

Our group is part of GWT steering committee, and the next generation of GWT is all about JUST these good parts. Basically removing or decoupling the early 2000 legacy and keeping only the good parts. In our opinion the best parts of GWT are:

* **Java to JavaScript transpiler:** extreme JavaScript performance due to compiling optimizations and static typing in the web;
* **java.* emulation: **excellent emulation of the main java libraries, providing runtime behavior/consistency;
* [**JS Interop**](https://speakerdeck.com/ederign/5-pillars-of-a-successful-java-web-application-1?slide=31)**: **almost transparent interoperability between Java <-> Javascript. This is a key aspect of the next generation of GWT and the Drools/jBPM platform: embrace and interop (two way) with JS ecosystem.

Google is currently working on a new transpiler called J2CL (short for Java-to-Closure, using the Google Closure Compiler) that will be the compiler used in GWT 3, the next major GWT release. The J2CL transpiler has a different architecture and scope, allowing it to overcome many of the disadvantages of the previous GWT 2 compiler.

Whereas the GWT 2 compiler must load the entire AST of all sources (including dependencies), J2CL is not a monolithic compiler. Much like javac, it is able to individually compile source files, using class files to resolve external dependencies, leaving greater potential for incremental compilation.

These three good parts are great and in our opinion, you should really consider using GWT as a transpiler in your web applications. But keep in mind that the most important point here is that GWT is just **our** first pillar implementation. You can consider using other transpilers like Typescript, Dart, Elm, ScalaJS, PureScript, or TeaVM.

The key point is that every web application should be handled as a large-scale application, and every large-scale application should be concerned about effective refactoring. The best way to achieve this is using statically typed languages.

---

# 2nd Pillar: Full stack Developers

The second pillar of every successful web application is related to developers’ skill sets: we should embrace the full stack. Your company may still differentiate backend and front-end developers, but gradually this border will vanish because in the end, we’re developers and developers should solve problems. Doesn’t matter if the problem is located on the server or in the browser because they are just problem-solving media.

The most efficient way to work in this full stack environment is to use the same programming model for backend and front-end. On our team, we embrace the Java EE programming model (and certainly we’re going to be a big player in the upcoming EE4J), but how are we able to share the same Java EE programming model in the browser?

For this we use the [Errai](http://erraiframework.org/) project. Leveraging the GWT compiler, Errai enables you to reuse existing Java EE (Eclipse EE) code on the client. With Errai, you can have dependency injection on your client-side code, observe and fire CDI events on the client, and exchange events between the client and server.

Having the same programming model among all the layers of our application, makes it evolve faster and safer, and especially, reduces the context switching between backend and frontend programming models. Learn all about Errai’s Java EE features [here](https://github.com/errai/errai-tutorial).

---

# 3rd Pillar: UX Integration

The next pillar for a successful web application is facilitating integration with your UX team. Your UX team is the one with the proper knowledge to build easily usable and visually attractive user interfaces. It’s not an engineering only job: these are different skillsets that have to work together to succeed.

Mixing HTML/CSS and control logic language is a mistake. We learned this in the hard way with the pain to maintain JSP pages.

Unfortunately, nowadays many JS frameworks are going to the same path:

<script src="https://gist.github.com/ederign/e9013bf9755dc81ccfa0b1aad85a6b5e.js"></script>

How can a UX expert work on this code? What is the impedance of having a programmer “translating HTML/CSS” into this framework specificities? Our industry keeps forcing UX to understand and interact with framework-specific code.

The 3rd pillar is that your web applications should respect and keep HTML and CSS as clean as possible. This is the only way to have a seamless integration between UX and engineers. But how to achieve this?

[Errai](http://docs.jboss.org/errai/latest/errai/reference/html_single/#sid-51806600) provides a pure HTML/CSS template based framework. With annotation processors, we bind transparently HTML tags to DOM Elements in java code, without introducing ANY change to HTML/CSS structure. With Errai UI, we do not mix and matches business logic with HTML/CSS

This is helpful for the Drools and jBPM teams because it allows a noiseless integration between the UX team and engineering. So the third pillar of a web application is to work closely with UX team and the only way to do this effectively is to leave the HTML and CSS as clean as possible.

This is the second of three posts about our 5 pillars of successful web applications. Stay tuned for the next one.

---


# 4th Pillar: 5~10 year Life-Span

The next pillar is how to make my web application last for more than 5~10 years. What’s the expected lifespan of your backend? Probably you don’t plan to throw it away in 2 years.

However, if you talk with some front-end engineers they answer will be slightly different and surprising. Some people said that you should expect to throw away your front-end code every two years, due to the evolution of JavaScript frameworks. Really? Should I rewrite the business logic of my front-end application every two years?

Making an application last is a well-known architecture challenge. Several architectural models share similar principles, i.e., Hexagonal Architecture by Alistair Cockburn, Onion Architecture by Jeffrey Palermo, Clean Architecture by Robert C. Martin. These principles are:

* Decoupled from Frameworks
* Testable
* Decoupled from UI
* Decoupled from Database
* Independent of external systems

In order to illustrate these principles, look on the following [Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html) diagram:

[![Clean Architecture](/assets/2018/cleanarchitecture.jpg "Clean Architecture")](/assets/2018/cleanarchitecture.jpg)

The entities and the uses cases should be should be protected from any external agent. This means that an external modification in a UI should never affect them. The real value of our applications is the business rules and the core logic that should be stable and only changed when a business changes.

The importance of this principle is clear to the backend developers. For instance, on AppFormer, we have a virtual file system API, it defines the contract for I/O operations.

[![AppFormer VFS](/assets/2018/appformervsf.jpg "AppFormer VFS")](/assets/2018/appformervsf.jpg)


This API is a NIO2 wrapper for I/O operations on the regular file system, or in distributed environments can be switched for a distributed GIT NIO2 backport. In that way, we can move from a simple file store to a distributed git backend without having to change any use case. How? Because we protected our use cases with a Virtual File System interface.

For backend developers, this is not new. It’s how we currently implement most of our backend architectures.

However, as industry, when we are architecting a front-end application do we have similar care? Or we just evaluate and adopt web frameworks and follow his model? Aren’t we relying on JS frameworks to define our web architectures?

The problem with that approach is that we need to decide the JS framework on the first day of the project. But the reality is that this will have to last to support business as long as business needs.

[![Curve](/assets/2018/curve.jpg "AppFormer VFS")](/assets/2018/curve.jpg)

But there is a caveat on this approach. There is a good chance that between 2nd and 4th year of JS framework of the day, the project will be canceled or will be replaced by a new version incompatible with the current one. Similar to the Angular 1.x and 2 [stor](https://toddmotto.com/future-of-angular-1-x)ies.

So what do we do? Do we rewrite the entire client code? Why do we think it’s ok to do this? And what is the risk of remaining in the old version? And the updates? How can I found resources to work with outdated tech? What about security risks? [Data breaches ](https://thehackernews.com/2017/09/equifax-apache-struts.html)for instance.

Robert C. Martin said that a good architecture allows volatile decisions to be easily changed. What if we dealt with the volatility of JS frameworks as a fact?

Our implementation for this problem is part of the Appformer project that Alex Porcelli and I are the leaders.

AppFormer (previously know as Uberfire) is the web-based workbench framework behind Red Hat JBoss Business Rules Management System (BRMS) and Red Hat JBoss BPM Suite (BPMS). AppFormer is also the basis for the next line of business of BRMS and BPMS platform: a low code/no code platform to develop modern business applications. Our initiative aims to allow business users easily build applications by mashing up components and connect them to other Red Hat modules and software.

Our main architectural goal is that nothing in our core business depends on any web framework. And how did we do this?

[![Architecture](/assets/2018/afarchitecture.jpg "AppFormer ARchitecture")](/assets/2018/afarchitecture.jpg)

We have created a programming model that has a well-defined component model based on Screen, Editors, Perspectives, and Popups. Each of these components has also a well-defined life-cycle.

In the user perspective, a Screen is a component. An editor is a component that is associated with a file type. A Perspective is a page.

[![Perrspectives](/assets/2018/perspectives.jpg "Perspectives")](/assets/2018/perspectives.jpg)

This is not new, it’s the old contract-based architecture. Each component is, in the end, a Java interface. And what are the advantages of this approach?

Do you remember that Errai has a Bean Manager in the browser? A well-defined programming model allows us to quickly switch between implementations of the component interface, instead of coupling with a specific web technology. We render the components based on the interface type and the bean name, not on the real implementation/framework.

[![Errai](/assets/2018/erraibean.jpg "Perspectives")](/assets/2018/erraibean.jpg)

We have legacy code, and such code were developed using old technologies, like GWT widgets, but when we modernize such implementations using pure HTML/CSS it’s just a matter of switch the implementations, because both implementations respect the same contract. That is the beauty of having a contract based model and CDI in the browser.

That is the how we managed to transparently run a gwt code from 7 years ago that implements the Screen interface, along with fresh code implemented in Errai UI.

So, this concludes the 4th pillars of successful web applications. You should prepare your architecture to live more than 2~4 years old life-cycle of JS frameworks, and in order to do that, your web architecture should be treated with the same respect as you treat your backend.

---



# 5th Pillar: Interoperability

And the last, but not least, the 5th Pillar of successful web applications is interoperability. You need to be flexible in order to stay modern. As we discussed in the 4th pillar, we need to have a solid architecture, but also we cannot be stuck in old tech and need to offer interoperability to my third parties. We need to embrace the new technologies. How can we do that?

We saw in the last pillar, that we use Java interfaces to define our components. In order to avoid boilerplate code, we use Java Annotations Processors to automatically generate adapters from user client to our interfaces. (i.e. @[WorkbenchPerspectives](https://speakerdeck.com/ederign/5-pillars-of-a-successful-java-web-application-1?slide=81) annotations trigger the generation for implementation of PerspectiveActivity interface).

To integrate with any external web framework, a new adapter that maps to the target interface and register needs to be implemented. Its implementation takes place in the Errai Bean Manager. After this, everything will become an implementation of the same contract and transparent for the use cases. [Here](https://speakerdeck.com/ederign/5-pillars-of-a-successful-java-web-application-1?slide=84) is an example of how we already do this with Angular code.

[![Errai](/assets/2018/errailookup.jpg "Errai Lookup")](/assets/2018/errailookup.jpg)


In this post we’ve presented the 5 pillars that we believe that are the foundation of every successful web application. Each of them, has already proved its value in practice in the development of Drools and jBPM workbenches.

Web applications are important pieces of our architecture. Although your application may not implement all these 5 pillars, you should keep them always in mind, because we really believe that all those 5 pillars provide a solid foundation for any web application.
