---
layout: post
title:  "Kogito Tooling 0.8.0 Released!"
permalink: /:year/:month/:day/:title:output_ext
date:   2020-11-13 00:00:00 -0500
---
We just launched a fresh new Kogito Tooling release! 🎉

On the [0.8.0](https://github.com/kiegroup/kogito-tooling/releases/tag/0.8.0) release, we made a lot of improvements and bug fixes. This post will do a quick overview of those. I hope you enjoy it!

## Kogito Tooling Examples Update!

We’re happy to announce a big update on the Kogito Tooling Examples in order to help you understand how to use and integrate the Kogito Tooling packages on your project!

[![Example](/assets/2020/example.png "Example")](/assets/2020/example.png)

The examples can be accessed here, the source code lives in this repository and you can follow this series of blog posts guiding you through them.

## BPMN and DMN Standalone Editors

We also published on [npm](https://www.npmjs.com/package/@kogito-tooling/kie-editors-standalone) the alpha version of our BPMN and DMN Standalone Editors. Now it’s super easy to embed our editors in your own applications:

<script src="https://gist.github.com/ederign/fab280b9ada5b57ce392b1a0ed6caf9d.js"></script>

[![Embed](/assets/2020/embed.png "Embed")](/assets/2020/embed.png)

See the full [blog post](https://blog.kie.org/2020/10/bpmn-and-dmn-standalone-editors.html) for details.

## DMN — Multiple Decision Requirement Diagrams

The [DMN editor](http://dmn.new/) was already great for expressing business logic and decomposing complex decisions into multiple nodes.

On 0.7.0, we introduced tech preview support for Multiple DRDs. On 0.7.1, we delivered the last bit of this important feature. Check this [post](http://karreiro.com/2020/10/13/dmn-editor-supports-multiple-diagrams-now.html) to understand this feature in detail.

[![DMN](/assets/2020/dmnm.gif "DMN")](/assets/2020/dmnm.gif)

## Update Gist on Online Modeler

We also included in this version a small but important tweak on Online Modeler. Now you can create gists and also update them!

[![GIST](/assets/2020/gist32.png "Gist")](/assets/2020/gist32.png)

## Kogito Tooling i18n Infrastructure

On the 0.7.1 release, we introduced a generic API for i18n in all the channels. Soon, editors will use this API to implement internationalization on all editors! Stay tuned.


## Fixed issues and improvements

We also made a lot of refactorings and improvements, especially to allow our internal API’s extendability.

### Infrastructure

* [[KOGITO-2926](https://issues.redhat.com/browse/KOGITO-2926)] — Provide readOnly property on EditorContext
* [[KOGITO-3709](https://issues.redhat.com/browse/KOGITO-3709)] — Creating GitHub gist with no token setup requires the users to click on “Gist it!” twice
* [[KOGITO-3347](https://issues.redhat.com/browse/KOGITO-3347)] — The input field on Gist modal is being marked as invalid with a valid token
* [[KOGITO-3705](https://issues.redhat.com/browse/KOGITO-3705)] — Cannot open files on private repos using the Chrome Extension
* [[KOGITO-3820](https://issues.redhat.com/browse/KOGITO-3820)] — Fix open from source Gist URLs double encoded

### Editors

* [[KOGITO-2348](https://issues.redhat.com/browse/KOGITO-2348)] — Scenario fails if model includes another one
* [[KOGITO-2773](https://issues.redhat.com/browse/KOGITO-2773)] — [Test Scenario Editor] BC — Kogito generated scesim file are in same cases not compatible
* [[KOGITO-3152](https://issues.redhat.com/browse/KOGITO-3152)] — [DMN Designer] PMML support — function parameters generation
* [[KOGITO-3571](https://issues.redhat.com/browse/KOGITO-3571)] — [DMN Designer] Multiple DRDs support — Information requirements are duplicated into the DMN XML
* [[KOGITO-1489](https://issues.redhat.com/browse/KOGITO-1489)] — Editor is broken after See as source during loading (Chrome Extension)
* [[KOGITO-3192](https://issues.redhat.com/browse/KOGITO-3192)] — [DMN Designer] Multiple DRDs support — The undo/reado are lost when user changes between diagrams
* [[KOGITO-3364](https://issues.redhat.com/browse/KOGITO-3364)] — [DMN Designer] Multiple DRDs support — When a node is deleted in the DRG, undo/redo operations do not work properly
* [[KOGITO-3366](https://issues.redhat.com/browse/KOGITO-3366)] — [DMN Designer] Boxed Expression — Decision Tables — Users lost constraints when they change the focus

## Further Reading/Watching

We had this month two talks on [KIE](https://www.youtube.com/channel/UCUjeymTM-TrwHs36388VRbw) youtube channel:

* [[KieLive#10] Introduction to Business Process core concepts](https://www.youtube.com/watch?v=F_ZD8mSZZsg&t=3290s&ab_channel=KIE), with Alessandro Lazarotti;
* [[KieLive#11] DMN for Developers](https://www.youtube.com/watch?v=66Q--bWibKQ&ab_channel=KIE), by Guilherme Carreiro.

I would like to also recommend a [blog post](https://blog.kie.org/2020/10/how-to-maintain-dmn-models-on-business-central-and-vscode.htm) from Guilherme, where he shows how to maintain DMN models on Business Central and VS Code.

## Thank you to everyone involved!

I would like to thank everyone involved with this release from the awesome KIE Tooling Engineers to the lifesavers QEs and the UX people that help us look awesome!

[
](https://medium.com/@ederign?source=post_sidebar--------------------------post_sidebar-----------)
