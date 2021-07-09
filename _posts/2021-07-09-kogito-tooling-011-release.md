---
layout: post
title:  "Kogito Tooling 0.11.0 Released!"
permalink: /:year/:month/:day/:title:output_ext
date:   2021-07-09 00:00:00 -0500
fav: false
---

We have just launched a fresh new Kogito Tooling release! 🎉 On the 0.11.0 [release](https://github.com/kiegroup/kogito-tooling/releases/tag/0.11.0), we made a lot of improvements and bug fixes. We are also happy to announce that this release marks the first release of our DMN Runner on [dmn.new](https://dmn.new/)!

This post will give a quick overview of this [release](https://github.com/kiegroup/kogito-tooling/releases/tag/0.11.0). I hope you enjoy it!

### Instantaneous Feedback Loop for DMN Authoring with DMN Runner

We’ve been exploring ways to augment the developer experience for our editors on the KIE Tooling team. Today, I'm proud to announce the release of our DMN Runner on dmn.new. We hope it will transform your DMN Authoring experience. Let’s see it in action:

For this reason, we decided to start a new development stream for our BPMN, DMN, and Scenario Simulator editors called [Kogito Editors](https://github.com/kiegroup/kogito-editors-java/), freeing the way for Editors to continue evolving on both streams separately (Kogito and BC) without carrying the weight of the other.

[![DMN runner](/assets/2021/runner32.gif "DMN Runner")](/assets/2021/runner32.gif)

Soon we will write a blog post describing this new awesome feature.

### New Features, fixed issues, and improvements

We also made some new features, a  lot of refactorings and improvements, with highlights to:

* [KOGITO-4136](https://issues.redhat.com/browse/KOGITO-4136) - Online Editor DMN Runner (First Iteration)
* [KOGITO-4043](https://issues.redhat.com/browse/KOGITO-4043) - The nodes should be created on top of the selected node in DMN editor
* [KOGITO-5132](https://issues.redhat.com/browse/KOGITO-5132)  - BPMN Editor - Improve SVG generated ids
* [KOGITO-3274](https://issues.redhat.com/browse/KOGITO-3274) - [DMN Designer] Read-only mode - Connectors appear differently on read-only mode
* [KOGITO-5115](https://issues.redhat.com/browse/KOGITO-5115) - Implement integration tests for Save operation in BPMN editor in VSCode
* [KOGITO-5135](https://issues.redhat.com/browse/KOGITO-5135) - [SceSim Designer] HiDPI is not working as expected
* [KOGITO-5142](https://issues.redhat.com/browse/KOGITO-5142) - [DMN/BPMN] Sync kogito-editors-java with latest translations
* [KOGITO-5378](https://issues.redhat.com/browse/KOGITO-5378) - Kogito Tooling VS Code extensions Workspaces Trust
* [KOGITO-5430](https://issues.redhat.com/browse/KOGITO-5430) - Prevent different envelopes in the same window to interact with each other
* [KOGITO-4671](https://issues.redhat.com/browse/KOGITO-4671) - New elements should always be connected by their central magnetic point
* [KOGITO-4980](https://issues.redhat.com/browse/KOGITO-4980) - Stunner - Palette fixes & improvements
* [KOGITO-3171](https://issues.redhat.com/browse/KOGITO-3171)  - Guided tour for invalid DMN models
* [KOGITO-3998](https://issues.redhat.com/browse/KOGITO-3998)  - It's not possible to save arrow edits
* [KOGITO-4712](https://issues.redhat.com/browse/KOGITO-4712)  - SceSim Editor does not work in Eclipse Theia
* [KOGITO-4935](https://issues.redhat.com/browse/KOGITO-4935)  - [BC included] [DMN/BPMN editor] Sometimes clicking outside doesn't unselect nodes
* [KOGITO-4977](https://issues.redhat.com/browse/KOGITO-4977)  - Stunner - Texts overlap toolboxes
* [KOGITO-5003](https://issues.redhat.com/browse/KOGITO-5003)  - [BC Included] DMN editor removing edges for duplicate Decision Nodes on canvas
* [KOGITO-5007](https://issues.redhat.com/browse/KOGITO-5007)  - Inconsistent results of integration tests across CI
* [KOGITO-5011](https://issues.redhat.com/browse/KOGITO-5011)  - Stunner - Unknown Custom tasks in Designer makes Diagram Explorer empty
* [KOGITO-5021](https://issues.redhat.com/browse/KOGITO-5021)  - Clear selection button doesn't work on Testing Tools when use click property first time.
* [KOGITO-5168](https://issues.redhat.com/browse/KOGITO-5168)  - Stunner - Editing text using Inline editor is shown over Properties panel or Expanded Palette
* [KOGITO-5169](https://issues.redhat.com/browse/KOGITO-5169)  - Stunner - The order of Custom tasks in the palette is different with every process opening


### Further Reading/Watching

We had some excellent blog posts on Kie Blog that I recommend you read:

* [Custom logic in BPMN](https://blog.kie.org/2021/06/custom-logic-in-bpmn.html), by Kirill Gaevskii;
* [DMN editor – Contributors Guide – Part 1](https://blog.kie.org/2021/06/dmn-editor-contributors-guide-part-1.html), by Guilherme Carreiro;
* [New DMN Boxed Expression Editor – What is in place](https://blog.kie.org/2021/06/new-dmn-boxed-expression-editor-what-is-in-place.html), by Valentino Pellegrino;

We also presented in some Kie Lives:

* [[KieLive#37] How to work with dashboards layouts](https://www.youtube.com/watch?v=pj8or38w2eQ&ab_channel=KIE), by William Siqueira;
* [[KieLive#36] How to play with DMN](https://www.youtube.com/watch?v=HQHjrf3i91Q&t=2258s&ab_channel=KIE), by Guilherme Carreiro;
* [[KieLive#35]Streaming decisions with DMN and Kafka](https://www.youtube.com/watch?v=pgj4jmkAl5A&ab_channel=KIE) , by Guilherme Caponetto.

### Thank you to everyone involved!

I would like to thank everyone involved with this release, from the excellent KIE Tooling Engineers to the lifesavers QEs and the UX people that help us look awesome!


[kie]