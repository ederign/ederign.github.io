---
layout: post
title:  "Kogito Tooling 0.7.0 Released!"
permalink: /:year/:month/:day/:title:output_ext
date:   2020-10-14 00:00:00 -0500
---
We just launched a fresh new Kogito Tooling release! 🎉
On the 0.7.0 [release](https://github.com/kiegroup/kogito-tooling/releases/tag/0.7.0), we made a lot of improvements and bug fixes.

This post will do a quick overview of those. I hope you enjoy it!

## Backend support on Kogito Tooling

We introduced Backend support on Kogito Tooling. Developers can now augment their editors' capabilities by connecting backend services through an infrastructure included in Kogito Tooling.

Lots of possibilities of executing code outside the client are enabled/facilitated with this new infrastructure, such as calling a java local backend service, reaching an HTTP endpoint, triggering a command in the terminal, to name a few.

Soon, this infrastructure will allow many new use cases, including auto-complete via Java Language Server, DMN/BPMN validations, Scenario Simulation executions, etc.

<iframe width="560" height="315" src="https://www.youtube.com/embed/qQkU5H-HTFE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

See full details of this important innovation in this [blog](https://medium.com/kie-foundation/backend-support-on-kogito-tooling-8be682a60b88) post from Guilherme Caponetto.

## DMN — Read-Only mode

We introduced a read-only version of our DMN Editor that will be really useful during PR reviews and also in your future embedded editors. Take a look at this feature on our [chrome extension](https://chrome.google.com/webstore/detail/mgkfehibfkdpjkfjbikpchpcfimepckf/publish-accepted?hl=en).

## DMN — Multiples Decision Requirement Diagrams

On 0.7.0, we are also introducing a tech preview support for Multiple DRDs. For complex DMN models, you can now use the DMN modeler to design multiple DMN decision requirements diagrams (DRDs) representing parts of the overall decision requirements graph (DRG) for a DMN decision model.

This improvement enables you to better organize DMN decision models with many decision requirements by dividing the model into smaller nested DRDs.

Check this [post](http://karreiro.com/2020/10/13/dmn-editor-supports-multiple-diagrams-now.html) to understand this feature in detail.

[![DMN](/assets/2020/DMN.gif "DMN")](/assets/2020/dmn.gif)

Notice: in some use cases, when your DMN model contains multiple decision requirements diagrams, you may face some validation errors that prevent the execution. You can put the kogito.decisions.validation=DISABLED property into the application.properties to disable model validation and successfully execute the model. This issue won’t be present on Kogito Tooling 0.7.1 (end of October) — KOGITO-3571.

## DMN — PMML support

We also added on DMN Editor, a new feature that enables PMML file imports inside DMN Editor. In a similar way we import external DMN files.

[![PMML](/assets/2020/pmml.png "PMML")](/assets/2020/pmml.gif)

A PMML file can be linked to a DMN file using the “Included Model” tab. Pressing the Include Model button, a popup with a selection box containing all PMML and DMN files inside the same directory of the opened DMN file should appear.

## BPMN — Script Syntax Highlight

The process designer now provides syntax highlighting and error checking capabilities when working with scripts, for example, in the case of a Script Task.

[![BPMN](/assets/2020/st.png "BPMN")](/assets/2020/st.png)

## BPMN & DMN — Inline Text Editing

Node name editing has been made more fluid with the new Inline Editor. It is possible to edit text directly on the nodes without floating boxes or confirmation buttons by double-clicking any node. For applying changes just hit “Enter” or click outside of the node and for canceling hit “Esc”, while editing.

[![BPMN](/assets/2020/st.gif "BPMN")](/assets/2020/st.gif)



## Fixed issues and improvements

We also made a lot of refactorings and improvements, especially to allow our internal APIs’ extendability.

### Infrastructure

* [[KOGITO-3313](https://issues.redhat.com/browse/KOGITO-3313)]: Fix on filename change
* [[KOGITO-3326](https://issues.redhat.com/browse/KOGITO-3326)]: Enable EmbeddedEditor to support an update on the StateControl instance
* [[KOGITO-3417](https://issues.redhat.com/browse/KOGITO-3417)]: EditorEnvelopeView reference should be get with a function to be updated
* [[KOGITO-1508](https://issues.redhat.com/browse/KOGITO-1508)]: Implement selenium test for kogito-bpmn in community
* [[KOGITO-1517](https://issues.redhat.com/browse/KOGITO-1517)]: Improve accessibility on file with unsupported extension error
* [[KOGITO-3042](https://issues.redhat.com/browse/KOGITO-3042)]: Replace MessageBusClient with proxified version of ApiToConsume
* [[KOGITO-3043](https://issues.redhat.com/browse/KOGITO-3043)]: Provide locale information in a way that GWT can read
* [[KOGITO-3056](https://issues.redhat.com/browse/KOGITO-3056)]: Move I18nService and and its Envelope/Channel APIs to its own module
* [[KOGITO-3057](https://issues.redhat.com/browse/KOGITO-3057)]: Add a initialLocale prop on I18nDictionariesProvider

### Editors

* [[KOGITO-2060](https://issues.redhat.com/browse/KOGITO-2060)]: [Test Scenario Editor] Order of facts of Test Tools in Kogito and BC is different
* [[KOGITO-1716](https://issues.redhat.com/browse/KOGITO-1716)]: [Test Scenario Editor] Show warning if user opens scesim file for rule based test scenario in VSCode
* [[KOGITO-3155](https://issues.redhat.com/browse/KOGITO-3155)]: [Test Scenario Editor] Test DMN model including PMML
* [[KOGITO-3153](https://issues.redhat.com/browse/KOGITO-3153)]: [DMN Designer] PMML support — run via Quarkus
* [[KOGITO-543](https://issues.redhat.com/browse/KOGITO-543)]: [DMN Designer] Read Only mode
* [[KOGITO-2664](https://issues.redhat.com/browse/KOGITO-2664)]: [DMN Designer] Multiple DRDs support
* [[KOGITO-3419](https://issues.redhat.com/browse/KOGITO-3419)]: [DMN Designer] None example of importing models in kie-dmn-core opens in editor
* [[KOGITO-3504](https://issues.redhat.com/browse/KOGITO-3504)]: Interrogation mark cannot be used on new inline editor

### VS Code

* [[KOGITO-3314](https://issues.redhat.com/browse/KOGITO-3314)]: Broken link on popup due to circular dependency issue
* [[KOGITO-2984](https://issues.redhat.com/browse/KOGITO-2984)]: Use i18n dictionaries on VS Code extension backend
* [[KOGITO-3205](https://issues.redhat.com/browse/KOGITO-3205)]: Create test runner service running on the backend infra

## Business Modeler Preview

* [[KOGITO-3336](https://issues.redhat.com/browse/KOGITO-3336)]: On Business Modeler Desktop the sample files are named as “unsaved file”
* [[KOGITO-2835](https://issues.redhat.com/browse/KOGITO-2835)]: Online — Update ‘edit existing file’ to use the FileUpdate component

### Known issues

* [[KOGITO-3571](https://issues.redhat.com/browse/KOGITO-3571)]: [DMN Designer] Multiple DRDs support — Information requirements are duplicated into the DMN XML

# Further Reading/Watching

If you are curious about the history of Kogito Tooling and how we created this technology, I would like to recommend two links for you:

* [Kogito Tooling history and Custom Envelopes](https://medium.com/kie-foundation/kogito-tooling-history-and-custom-envelopes-c35736a40cba), a blog post written by Tiago Bento;
* [Multiplying Architecture](https://www.youtube.com/watch?v=Dvz0bGa9oh8&t=4s), a presentation that Eder Ignatowicz gave on [KIE](https://www.youtube.com/channel/UCUjeymTM-TrwHs36388VRbw) youtube channel;

## Thank you to everyone involved!

I would like to thank everyone involved with this release from the awesome KIE Tooling Engineers to the lifesavers QEs and the UX people that help us look awesome!
