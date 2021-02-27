---
layout: post
title:  "What is new on Business Central, from Foundation Team perspective — June 2019"
permalink: /:year/:month/:day/:title:output_ext
date:   2019-07-06 00:00:00 -0500
---
Recently, we pushed a lot of cool new features on Business Central added by Foundation Team. Those features will be soon available on 7.23 release.

This post will do a quick overview of those. I hope you guys enjoy!

## Role Based Access Control for Branches

Built upon [Contributors feature](https://medium.com/kie-foundation/contributors-on-business-central-c3f9647f378a), we are proud to release role-based access branches on Business Central.

With this new feature, we will provide a new UI on project settings in order to allow users to restrict the access for a target branch for a specific collaborator type. This is pretty useful for instance when you want to freeze a release branch for some roles. Take a look at the demo:

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZNh5mELLZF4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Keep in mind that for now, the security check is using both sources (Security Management screen and contributors) to grant or deny permissions to spaces and projects (Inclusive OR). One example of this is where the user has the security permission to update a project and/or has write permission on that branch (based on the contributor type), then he or she will be able to create new assets. These are our security configurations for this demo:

[![Security Management](/assets/2019/security.jpg "Security Management")](/assets/2019/security.jpg)

## Import specific branches on Business Central

Sometimes you don’t want to import all the branches from your repo and now it’s possible to import just what you want:

<iframe width="560" height="315" src="https://www.youtube.com/embed/gaWpOTGuilA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Keep in mind that master branch is mandatory for Business Central.

## Form modeler support for class models from external dependencies

With this [PR](https://github.com/kiegroup/kie-wb-common/pull/2525) from Pere, we are able to load on forms models from external dependencies. This allows us to generate forms for processes that use classes from external dependencies (not created on the same project with Data Modeler but that are added as dependencies of the project).

This change also fixes an issue on DMO when resolving the TypeSource from external DO.

## Upload of multiple documents for human task forms

A new widget called “Document Collection” is available in the forms designer. It enables you to upload multiple documents to a process or task form. You can also use the “Document Collection” widget for process or task forms that have a variable with the type `org.jbpm.document.DocumentCollection`. Additionally, it also supports the legacy type `org.jbpm.document.Documents`.

## Dashbuilder C3 Charts extended support and Drop GCharts

We just reached C3 full feature compatibility with our old GCharts renderer and from now on, Business Central uses a new API for chart rendering based on C3 and D3.

The C3 Renderer API is now used by default and implements all features from the previous chart library, Google Charts. The Google Charts library is now deprecated and removed from BC due to some implementation issues (non-open source and also requires online access). To revert it to Google Charts, build it from sources and add it to Business Central (see the `README.md` file in `dashbuilder-renderer-google` repository), and then set the renderer system property to `org.dashbuilder.renderer.default=gwtcharts`.

[![Dashbuilder](/assets/2019/db1.jpg "Dashbuilder")](/assets/2019/db1.jpg)

## CSS Editor on Form Builder

We also included a cool new CSS Editor on our Form Builder. Take a look at your demo:

<iframe width="560" height="315" src="https://www.youtube.com/embed/dsZn84UdsWE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Thanks for reading! Stay tuned for our next updates!

I hope this could be useful for you — or just fun to read ;) ! 💖
