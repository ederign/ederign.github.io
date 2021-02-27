---
layout: post
title:  "Kogito Tooling Release: DMN support and Chrome Extension PRs visualization"
permalink: /:year/:month/:day/:title:output_ext
date:   2019-10-22 00:00:00 -0500
---
We are happy to announce a fresh new [Kogito Tooling release ](https://github.com/kiegroup/kogito-tooling/releases/tag/0.2.0)that includes a major milestone for our team — the DMN support for VSCode and GitHub Chrome extension.

We also added some important enhancements to our GitHub Chrome Extension. Now users will be able to not just edit but also visualize DMN/BPMN diagrams — what is especially cool on Pull Request reviews.

First, as always, let’s take a look at the demo! Please pay special attention to the pull request workflow.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZjzlhOWBPSc" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Awesome isn’t it? Alex Porcelli wrote a detailed post about how this feature is a game changer to the BPMN/DMN developer workflow. Take a look on his [blog](https://porcelli.me/announcement/tooling/github/bpmn/dmn/2019/10/22/bpmn-dmn-github-extension.html).

## Decision Model and Notation Support

With a great collaboration of the Drools Tooling team (with highlights for the impressive work of Michael Anstis, Gabriele Cardosi and Guilherme Carreiro Gomes) we reached a major milestone on Kogito tooling. Now you will be able to create your DMN files inside your VSCode and on GitHub Chrome Extension.

[![DMN Chrome](/assets/2019/ex-dmn.gif "DMN Chrome")](/assets/2019/ex-dmn.gif)

## Chrome Extension New Features

As promised in the last post, we also added on this release two new major improvements on our Chrome Extension. The ability to visualize the BPMN/DMN diagram on any repo (not only on editing) and also a great integration to the GitHub PR review mechanism.

[![DMN Chrome](/assets/2019/ex-dmn1.gif "DMN Chrome")](/assets/2019/ex-dmn1.gif)

You are now able to not only visualize the current diagram but if you click on the original button, you will be able to see the current state of the file in the repository. We hope that this will be helpful to review your models directly on the GitHub Pull Request in the same way you do for any source code.
NOTE: When editing a file directly on GitHub’s interface and committing it, GitHub takes a while to make the new file available on raw.githubusercontent.com. Since that’s where we fetch the files from, you might see outdated versions for a while. Don’t panic! After a few moments the files will be in sync.


## But how to install this?

Ok, this is cool but how to install it? Look at the instructions on our blog posts: [How to setup the extension on Chrome Extension](https://medium.com/kie-foundation/bpmn-chrome-extension-released-alpha-abe89676d76) and [How to set up the extension on VSCode](https://medium.com/kie-foundation/bpmn-vscode-extension-released-alpha-1782ddaa2a4e). Soon we will make this process more straight forward publishing on Chrome and VSCode extension store.

## What’s Next

As you may have realised, we have big plans for our kogito tooling. Soon, we will hope to release another game-changing tool for you! Stay tuned!
