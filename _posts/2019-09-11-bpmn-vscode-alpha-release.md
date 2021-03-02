---
layout: post
title:  "BPMN VSCode Extension Released (alpha)"
permalink: /:year/:month/:day/:title:output_ext
date:   2019-09-11 00:00:00 -0500
fav: true
---

We are really happy to announce the alpha release of our first VSCode extension: the BPMN editor. This release marks the first piece of the new tooling infrastructure for the Kie Group Team.

Before diving on details, let’s take a look at a quick demo of this feature:

[![VS Code Alpha](/assets/2019/vscode.gif "VS Code Alpha")](/assets/2019/vscode.gif)


Pretty cool isn’t it?

This is a group effort, but I would like to highlight the work done by Alex Porcelli, Tiago Bento, Paulo Martins, William Siqueira from the foundation team; Roger Martinez and Tiago Dolphine from Stunner Team (the guys behind BPMN Editor) and also Sarah Rambacher and Joachim Schuler from UX team.

With VSCode support, our goal is to streamline the dev workflow of our platform, making it easy for developers to create BPMN diagrams and push them straight to [kogito runtimes](https://github.com/kiegroup/kogito-runtimes). If you’re interested to understand the whole developer workflow, Alex Porcelli wrote a [blog post ](https://porcelli.me/announcement/tooling/vscode/bpmn/2019/09/11/new-vscode-gui-editor.html)where he builds a Kogito application from scratch and deploys it to the cloud.

But how to install it?

## How to set up the extension on VSCode

During this alpha stage, you will have to download the extension from our GitHub [releases page](https://github.com/kiegroup/kogito-tooling/releases) and install it manually on VSCode. Soon we will publish this extension on VSCode Marketplace, but for now, those are the installation steps:

[![VS Code Alpha](/assets/2019/vscode1.gif "VS Code Alpha")](/assets/2019/vscode1.gif)


## What’s Next

In the following days, Tiago Bento will write a post with a deep dive into the architecture, and also provides a quick tutorial of how to create your own graphical user interface editor for VSCode using ReactJS.

Soon we will release a DMN editor extension under the same platform, stay tuned!

## Known issues

We are really happy with the results of this alpha release and we want to get the community involved in this as early as possible, that is why we released this with some known issues:

* [AF-2167 Native VSCode keybindings](https://issues.jboss.org/browse/AF-2167): we still need to work on some key bindings for VSCode, i.e. undo-redo and copy and paste on OSX environments (we bind control instead of command key);
* [AF-2113 Add a “dirty” indicator on editors](https://issues.jboss.org/browse/AF-2113): currently, there is no indicator of a file that requires a save;
* [AF-2168 No confirmation on closing dirty file](https://issues.jboss.org/browse/AF-2168): right now, if you close a dirty editor, it will close without requiring confirmation;
* [KOGITO-224 Stunner — Press ENTER to define a type](https://issues.jboss.org/browse/KOGITO-224): users should be able to define a new type pressing enter;
* [KOGITO-225 Stunner — Reuse inputted types in different places within the diagram](https://issues.jboss.org/browse/KOGITO-225);
* [KOGITO-226 Stunner — Show an error dialog when using non-supported elements](https://issues.jboss.org/browse/KOGITO-226): if you try to open a file that contains an unsupported element, we provide an error. Please open a JIRA for it!
* [KOGITO-272](https://issues.jboss.org/browse/KOGITO-272) Editor doesn’t close when file is deleted.

[Pull requests](https://github.com/kiegroup/kogito-tooling), [bug reports](https://issues.jboss.org/projects/KOGITO/summary) are more than welcome, please remember this is an ongoing effort of our community!

## Take-Away

As I already said, we are really happy to release this extension. Soon we will provide new editors under this platform! Exciting times ahead!
