---
layout: post
title: "Comparing Choices in DMN Modeling"
permalink: /:year/:month/:day/:title:output_ext
date: 2022-10-04 00:00:00 -0500
fav: true
---

Recently in a [blog post](https://social-biz.org/2022/10/03/choices-in-modeling-dmn/), Keith Swenson, VP of R&D Fujitsu America and former leader of the DMN "Technical Compatibility Kit," did a comparative analysis between free DMN modeling alternatives.

The author compared TrisoTech DMN Modeler, Camunda, Red Hat Drools Workbench, and our beloved KIE Sandbox. As the results are interesting, I've decided to share them in a blog post.

### Little Background: Kie Sandbox and DMN 'runner'

Started with a prototype in late 2020, aiming to explore ways to augment the developer authoring experience for BPMN and DMN assets; [KIE Sandbox](https://sandbox.kie.org/) gradually got traction and became an integrated part of our Tooling experience.  
Check out this [blog post](https://ederign.me/2022/02/03/kie-sandbox.html) for a walkthrough of the top features of KIE Sandbox.

[![Sandbox](/assets/2022/kiesandbox1.gif "Sandbox")](/assets/2022/kiesandbox1.gif)

Focusing on a seamless authoring experience and an instantaneous feedback loop for DMN models, the DMN runner was [launched](https://ederign.me/2021/07/12/dmn-runner-released.html) mid-2021, and quickly became one of my favorite innovations on Tooling.

[![Runner](/assets/2022/kiesandboxrunner.gif "Runner")](/assets/2022/kiesandboxrunner.gif)

Using a fast and automatic form generation and evaluation based on DMN models, DMN runner allows users to quickly try and experiment with their DMN runner in authoring, emulating an experience similar to authoring a spreadsheet like Excel or Google Docs.

[![Runner1](/assets/2021/dmnrunner4.gif "Runner1")](/assets/2021/dmnrunner4.gif)

### Comparing Choices in Modeling DMN

In a recent [blog post](https://social-biz.org/2022/10/03/choices-in-modeling-dmn/), Keith Swenson provided the following feedback from our tools:

> What is particularly impressive is the DMN test capability. To get it to run, you need to download and start the KIE Sandbox Extended Services, which ran without a hitch. The web UI automatically noticed that the engine was installed. Then, it would automatically generate forms for inputting the data. Most impressive was that it can handle structured data records and arrays, even arrays of structured records. The output appears in the next column over. The complex table and list commands all ran. It is hard for me to really express how great it was after days of trying to get various combinations to work, to find an environment where everything ran without a problem.
> So, if you want practical experience with DMN models and running the models, go right to KIE Sandbox. It works.
> -- <cite>Keith Swenson</cite>

The author also summarizes that among other competitors, KIE Sandbox is the "best all around tool for a DMN practitioner, and built on RedHat so certainly compatible with that."

Keith Swenson, our tooling team, would like to thank you for the feedback, and we are looking forward to ways to improve even more our Tooling!

[kie]
