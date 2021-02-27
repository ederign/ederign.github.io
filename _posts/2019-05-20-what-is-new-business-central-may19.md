---
layout: post
title:  "What is new on Business Central, from Foundation Team perspective — May 2019"
permalink: /:year/:month/:day/:title:output_ext
date:   2019-05-20 00:00:00 -0500
---
Recently, we released a lot of cool new features on Business Central added by Foundation Team. This post will do a quick overview of those. I hope you guys enjoy!

## Business Central Consolidation

KIE (Knowledge Is Everything) is an umbrella brand offering a complete portfolio of solutions for business automation. It contains a group of related projects including Drools (business rule management system), jBPM (a flexible Business Process Management Suite) and OptaPlanner (constraint solver).

The web tooling to interface and integrate with those projects are also provided on KIE and used to be referenced as Workbench: a web UI that you can author, manage and track business rules and processes.

In an effort to consolidate and promote better our technology stack, we just included on 7.18 a consolidation and rebranding of these workbenches to a single distribution called to **Business Central** (accessible via /business-central). Take a look at this [post](https://medium.com/kie-foundation/workbench-consolidation-and-profiles-7f6ee0ef401) to do a deep dive on this migration.

[![Business Central](/assets/2019/bc.jpg "Business Central")](/assets/2019/bc.jpg)

## Offline Charts

The Dashbuilder default chart implementation was replaced from Google Charts to [C3.js](https://c3js.org/). The main reason behind this move is to allow our users to use Business Central in an offline environment (Google Charts requires internet connection).

We also have future plans to completely deprecate Google Charts on future versions.

[![Dashbuilderl](/assets/2019/db.jpg "Dashbuilderl")](/assets/2019/bc.jpg)

## Streamline the Dev Workflow on Business Central

Based on feedback from our community, one of our current main goals on BC is to enhance the developer workflow for rules/BPM.

Some releases ago, we already delivery [multiple branches support](https://medium.com/kie-foundation/branch-support-on-business-central-b551fd1939f1) on Business Central:

[![Dev Flow](/assets/2019/devflow.gif "Dev Flow")](/assets/2019/devflow.gif)

### Git Hooks Samples

We also delivered some time ago some cool [examples](http://porcelli.me/rhba/business-central/git/githook/integration/push/2018/12/06/business-central-git-hook-push.html) to make it easier for you to automate git workflows via git hooks. You should take it a [look](http://porcelli.me/rhba/business-central/git/githook/integration/push/2018/12/06/business-central-git-hook-push.html).

<iframe width="560" height="315" src="https://www.youtube.com/embed/jL-Htol-9vg" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



### Git Hooks Execution Feedback Messages

Based on your feedback on our git hooks integration, we included on 7.18 a way to customize your own messages on script execution.

[![Git Hooks](/assets/2019/githook.gif "Dev Flow")](/assets/2019/githook.gif)


Business Central now provides a mechanism to enable users getting feedback about the git hooks execution using customized messages based on the hook exit code. Stay tuned for a blog post about this feature.

### SSH Keystore

In order to provide better automation on our platform, we delivered in the Business central an SSH Keystore. Basically, this means that users can store their public keys inside workbench and use them to authenticate their automation scripts via ssh keys.

[![SSH](/assets/2019/ssh.gif "Dev Flow")](/assets/2019/ssh.gif)


Stay tuned for a blog post about this feature.

### Permissions on Authoring

Soon, we will delivery in Business Central a so desired feature called Role-Based Access Control to branches. This will allow our users to fine-tune “who can do what” on the business central authoring environment. One example of the future use of this feature is to lock a release branch.

But on the foundation team, we focus on steady and incremental deliveries. On 7.18 we delivered the first step towards RBAC, that are permissions in authoring.

Basically, we created three roles integrated directly into spaces and projects (Contributor/Admin/Owners). This will allow you to fine-tune the permissions on your spaces and projects and soon this will deprecate Security Permissions for spaces and projects on preferences. Take a look a [full post](https://medium.com/kie-foundation/contributors-on-business-central-c3f9647f378a) about this change.


<iframe width="560" height="315" src="https://www.youtube.com/embed/hNRmq9O0Wlo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



### Speed up the Developer Workflow

As I already mentioned, one of our goals is to enhance the developer workflow for rules/BPM. And on 7.18 release we included two things that we believe that will be game changers for those developers who work with Business Central on a daily basis.

The first feature is the ‘Build and Install’ button on authoring. This allows users to do a build on their projects without the need of a deploy.


[![Dev Workflow](/assets/2019/devw.gif "Dev Flow")](/assets/2019/devw.gif)


The second important addition is that we created two new Decision/Process Server Modes. DEVELOPMENT (the new default) and PRODUCTION that (Blocks “-SNAPSHOT” deployment).

This changes will allow users to quickly build, deploy our projects, making it easier (and saving a lot of clicks) to test their changes on Kie Server while we can preserve the production consistency. First, let’s take a look in our production mode.

[![Dev Workflow](/assets/2019/devw2.gif "Dev Flow")](/assets/2019/devw2.gif)


Now, if the Kie Server is on the development mode and the project is also on development mode (-SNAPSHOT) you have two new options:

* Deploy: no questions to deploy if the server is on Development Mode and preserves server data;
* Redeploy: no questions to deploy if the server is on Development Mode and clean server data.

Take a look at a video of this feature and stay tuned for future blog posts:


<iframe width="560" height="315" src="https://www.youtube.com/embed/e3HXuTxp7g4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Thanks for reading! I hope this could be useful for you — or just fun to read ;) ! 💖
