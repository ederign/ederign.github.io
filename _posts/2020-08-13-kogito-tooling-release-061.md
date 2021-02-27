---
layout: post
title:  "Kogito Tooling 0.6.1 Released!"
permalink: /:year/:month/:day/:title:output_ext
date:   2020-08-13 00:00:00 -0500
---
We just launched a fresh new Kogito Tooling release! 🎉
On [0.6.1](https://github.com/kiegroup/kogito-tooling/releases/tag/0.6.1) release, we made a lot of improvements and bug fixes. This post will do a quick overview of those. I hope you enjoy it!

## Kogito Tooling CI Improvements

Since the beginning of the project, we have been using GitHub Actions to [build](https://github.com/kiegroup/kogito-tooling/pull/246/checks) kogito tooling repositories, but last week we added three significant improvements for our CI/CD on this release.

## Daily builds of our kogito tooling

Some days ago, we started doing an automatic daily release of the kogito tooling. The daily build of the Business Modeler can be accessed on this [link](https://kiegroup.github.io/kogito-online/dev/#/) and other artifacts (VS Code, Desktop, Hub, and Chrome Extension) can be downloaded in the latest [“Publish daily dev version”](https://github.com/kiegroup/kogito-tooling/actions?query=workflow%3A%22Publish+daily+dev+version%22) job. This is a nice feature to try the latest master features of kogito tooling! 🚀

## Business Modeler build for each PR

Also, to improve tests and code review processes, now for each PR on kogito-tooling instead of just generating the build artifacts, we are also providing a live version of Business Modeler.
To access the Business Modeler for a job fired by a PR in kogito-tooling, you can use https://kiegroup.github.io/kogito-online-ci/pull/<PR_NUMBER>
To access the Business Modeler for a job fired by a comment in the kogito-tooling issue, you can use https://kiegroup.github.io/kogito-online-ci/comment/<COMMENT_ID>

## Build RHPAM Editors on kogito tooling actions

The BPMN, DMN, and Scesim editors used on Kogito are based on RHPAM editors that live on kie-wb-common and drools-wb Java-based repositories.
Another significant improvement that we did on this release is kogito-tooling GitHub Actions to do a full build on RHPAM editors and generate an integrated artifact (kogito tooling + editors from Java repositories).
Now, it’s just a matter of the author of a PR in kogito-tooling using a branch with the same name in his/her fork that contains changes in any editor (BPMN, DMN, or SceSim). As soon this happens, the “Pull Request CI — Full Downstream” job will run and produce a build of the VS Code extension, Business Modeler, Chrome Extension, and Desktop with the modified editors for faster testing.
But how should I build kogito tooling, if my editor change doesn’t affect the kogito tooling repository? Go to the pinned issue on the kogito-tooling repo and create a new comment following the format “Build: {github-username}/{branch-name}”.

[![Build](/assets/2020/build.png "Build")](/assets/2020/build.png)

In my opinion, those three improvements are a huge step forward for us. First, they will speed up a lot of our code review process and build, and, most important, it’s a big step forward in the path to continuous delivery of our lovely Business Modeler.

## Kogito Tooling i18n

We’re happy to announce that Kogito Tooling is ready to be internationalized! This means that it will be possible to change the locale and access the Kogito Tooling Channels’ translations.

<script src="https://gist.github.com/ljmotta/4a3533c1907593ea0046222c577ca77b.js"></script>

We developed an i18n type-safe library with React usability in mind to enable this new feature, which allows simple and easy integration with an already existing project. See the full details on this blog post.

## Page Support on OmniChannel Architecture

Since its inception, OmniChannel allowed us to run the same editor code in multiple channels without changing the codebase. Now we enhance this architecture also to support Pages and Components.

This new architectural component will enable many new use cases, as an example showing runtime screens, dashboards, etc. Stay tuned that soon we will launch a blog post and some examples of how to use it.

[![Page](/assets/2020/page.png "Page")](/assets/2020/page.png)

## Auto start property for ad-hoc subprocess

We also added add “Auto Start” property to Adhoc sub-process properties panel, which is currently supported by the Kogito runtime via metadata.

[![Start](/assets/2020/start.png "Start")](/assets/2020/start.png)



## Fixed issues and improvements

We also made a lot of refactorings and improvements, especially to allow our internal APIs’ extendability.

* [[KOGITO-2496](https://issues.redhat.com/browse/KOGITO-2496)] — Review exports on microeditor-envelope/index.ts
* [[KOGITO-2833](https://issues.redhat.com/browse/KOGITO-2833)] — Remove Enzyme as snapshot serializer
* [[KOGITO-2212](https://issues.redhat.com/browse/KOGITO-2212)] — Update the close warning box
* [[KOGITO-2495](https://issues.redhat.com/browse/KOGITO-2495)] — Make it possible for channels to copy keyboard shortcuts from the envelope
* [[KOGITO-2573](https://issues.redhat.com/browse/KOGITO-2573)] — Make React and ReactDOM be peerDependencies on @kogito-tooling/core-api
* [[KOGITO-2601](https://issues.redhat.com/browse/KOGITO-2601)] — Move State Control API to kie-bc-editors
* [[KOGITO-2877](https://issues.redhat.com/browse/KOGITO-2877)] — Improve EmbeddedEditor and EmbeddedView usage experience
* [[KOGITO-924](https://issues.redhat.com/browse/KOGITO-924)] — Improve Kogito Tooling CI
* [[KOGITO-2815](https://issues.redhat.com/browse/KOGITO-2815)] — Improve creation of Editor packages
* [[KOGITO-735](https://issues.redhat.com/browse/KOGITO-735)] — Make Chrome Extension and Online Editor point to the same static resources on kogito-online
* [[KOGITO-925](https://issues.redhat.com/browse/KOGITO-925)] — Online Editor deploy for every CI build
* [[KOGITO-926](https://issues.redhat.com/browse/KOGITO-926)] — Chrome Extension Should Point to a Specific Editor Version
* [[KOGITO-2209](https://issues.redhat.com/browse/KOGITO-2209)] — Promisify all the envelope calls
* [[KOGITO-2224](https://issues.redhat.com/browse/KOGITO-2224)] — Add yarn.lock updated check
* [[KOGITO-2512](https://issues.redhat.com/browse/KOGITO-2512)] — Prepare and use the patternfly-base lib where applicable
* [[KOGITO-2547](https://issues.redhat.com/browse/KOGITO-2547)] — Refactor asWebviewUri on vscode-extension project
* [[KOGITO-2659](https://issues.redhat.com/browse/KOGITO-2659)] — Update PatternFly to the latest version
* [[KOGITO-2696](https://issues.redhat.com/browse/KOGITO-2696)] — Add error treatment to promisified envelope calls
* [[KOGITO-2821](https://issues.redhat.com/browse/KOGITO-2821)] — Rename Router interface and remove the dependency of Editor packages in channels
* [[KOGITO-2822](https://issues.redhat.com/browse/KOGITO-2822)] — Provide locale information to Editors
* [[KOGITO-2892](https://issues.redhat.com/browse/KOGITO-2892)] — Integrate the i18n package on the Desktop, Hub and Chrome Extension
* [[KOGITO-2982](https://issues.redhat.com/browse/KOGITO-2982)] — Create a subscription mechanism to enable inter-page communication
* [[KOGITO-2983](https://issues.redhat.com/browse/KOGITO-2983)] — Create a generic Envelope class to define your page type

And we solved a bunch of issues:

### VS Code

* [[KOGITO-2579](https://issues.redhat.com/browse/KOGITO-2579)] — Custom Editor VS Code issues on 1.46 version (probably fixed on 1.47)
* [[KOGITO-1689](https://issues.redhat.com/browse/KOGITO-1689)] — Save when multiple assets opened
* [[KOGITO-2134](https://issues.redhat.com/browse/KOGITO-2134)] — [VSCode] Allow custom editors to hook into Edit menu actions
* [[KOGITO-2135](https://issues.redhat.com/browse/KOGITO-2135)] — [VSCode] Custom editor does not open properly
* [[KOGITO-2619](https://issues.redhat.com/browse/KOGITO-2619)] — scrolling a nested Decision Table in VSCode DMN Editor messed up the editor screen
* [[KOGITO-1915](https://issues.redhat.com/browse/KOGITO-1915)] — Error message doesn’t appear when VS Code is launched externally
* [[KOGITO-1980](https://issues.redhat.com/browse/KOGITO-1980)] — Update labels from VSCode to VS Code

### Business Modeler

* [[KOGITO-2432](https://issues.redhat.com/browse/KOGITO-2432)] — Downloaded file from online editor keeps “new-file” as model name in DMN models
* [[KOGITO-2810](https://issues.redhat.com/browse/KOGITO-2810)] — In the online editor, the filename in header toolbar is not accessible
* [[KOGITO-2954](https://issues.redhat.com/browse/KOGITO-2954)] — Use the file extension to render the content on EditorToolbar

### Editors

* [[KOGITO-1883](https://issues.redhat.com/browse/KOGITO-1883)] — [Test Scenario Editor] Search DMN files over subfolders doesn’t work in Windows Environment
* [[KOGITO-2953](https://issues.redhat.com/browse/KOGITO-2953)] — Fix Guided Tour styles

## Thank you to everyone involved!

I would like to thank everyone involved with this release from the awesome KIE Tooling Engineers to the lifesavers QEs and the UX people that help us look awesome!
