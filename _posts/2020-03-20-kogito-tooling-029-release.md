---
layout: post
title:  "Kogito Tooling 0.2.9/0.2.8 Alpha Release"
permalink: /:year/:month/:day/:title:output_ext
date:   2020-03-20 00:00:00 -0500
---
We are happy to announce a fresh Kogito Tooling release!

On this [release](https://github.com/kiegroup/kogito-tooling/releases), we did a lot of improvements and bug fixes. We progressed a lot on the DMN/BPMN Editors, delivered a brand new UX for the Online Editor and also improved a lot the ‘native’ experience of VSCode.

Another important milestone achieved is the first experimental release of our extension with the of the new [VSCode Custom webview proposed API](https://github.com/microsoft/vscode/issues/77131). In order to give it a try, you will need to download the latest version of VSCode (1.43.0), install the specific extension (vscode_extension_kogito_kie_editors_0.2.8-new-webview-api-release.vsix) and run it with the following command:

<script src="https://gist.github.com/ederign/401eb69852a6d6d7c5c2dfd90ebd0c36.js"></script>

In case you don’t want to run VSCode in proposed API mode, for now, we are still packing vscode_extension_kogito_kie_editors_0.2.8.vsix. Included on this release:


## DMN Editor Improvements/Bug Fixes

* [KOGITO-964](https://issues.redhat.com/browse/KOGITO-964): Run on VSCode all DMN demos published on Kogito examples
* [KOGITO-542](https://issues.redhat.com/browse/KOGITO-542) DMN — Format the output XML
* [KOGITO-295](https://issues.redhat.com/browse/KOGITO-295) [DMN Designer] Kogito — DMNMarshaller — Integrations Tests on gwt-jsonix-marshallers
* [KOGITO-936](https://issues.redhat.com/browse/KOGITO-936) Analyse why editor increased the artifact size
* [KOGITO-778](https://issues.redhat.com/browse/KOGITO-778) [DMN Designer] Client-side marshaling tests
* [KOGITO-841](https://issues.redhat.com/browse/KOGITO-841): Documentation Links popup is not readable in DMN VS Code Extension
* [KOGITO-1155](https://issues.redhat.com/browse/KOGITO-1155): Fix Kogito examples with namespaces from other vendors
* [KOGITO-1156](https://issues.redhat.com/browse/KOGITO-1156): [DMN Designer] Documentation — Buttons (Download, Print) do not work on VSCode
* [KOGITO-1157](https://issues.redhat.com/browse/KOGITO-1157): [DMN Designer] New models must be named with the file name on VSCode
* [KOGITO-1337](https://issues.redhat.com/browse/KOGITO-1337) [DMN Designer] Author and filename are always non defined

## BPMN Improvements/Bug Fixes

* [KOGITO-631](https://issues.redhat.com/browse/KOGITO-631) BPMN files created in VSCode contain invalid id
* [KOGITO-653](https://issues.redhat.com/browse/KOGITO-653) Support process type (Public/Private) in Stunner
* [KOGITO-257](https://issues.redhat.com/browse/KOGITO-257) — Condition Expression should … only “Expression” option
* [KOGITO-980](https://issues.redhat.com/browse/KOGITO-980) Error message adding a condition expression
* [KOGITO-1177](https://issues.redhat.com/browse/KOGITO-1177) Kogito Quick Starts Scripts / Kafka Examples Spring Boot
* [KOGITO-1191](https://issues.redhat.com/browse/KOGITO-1191) Kogito Quick Starts Scripts / Timers issue with cancelsActivity

## Online Editor Improvements

* [KOGITO-741 ](https://issues.redhat.com/browse/KOGITO-741)Bring Octokit support to Online Editor
* [KOGITO-736 ](https://issues.redhat.com/browse/KOGITO-736)Add link to online editor on GitHub file list
* [KOGITO-740 ](https://issues.redhat.com/browse/KOGITO-740)Update README with development instructions for online-editor
* [KOGITO-734 ](https://issues.redhat.com/browse/KOGITO-734)Remove scroll from pages on both Chrome and Safari
* [KOGITO-860](https://issues.redhat.com/browse/KOGITO-860) Add error alerts for when Online Editor fails to open a file URL
* [KOGITO-861](https://issues.redhat.com/browse/KOGITO-861) Add a input to paste a file URL in the Online Editor home page
* [KOGITO-932 ](https://issues.redhat.com/browse/KOGITO-932)Implement revised online editor landing page
* [KOGITO-1009 ](https://issues.redhat.com/browse/KOGITO-1009)Implement revised online editor masthead
* [KOGITO-737](https://issues.redhat.com/browse/KOGITO-737) Opening online editor for the second time doesn’t take the updated name in consideration
* [KOGITO-1280](https://issues.redhat.com/browse/KOGITO-1280) .new Domain Setup

## VSCode Improvements

* [KOGITO-883 ](https://issues.redhat.com/browse/KOGITO-883)VSCode Integration: Make undo/redo work with existing VSCode commands
* [KOGITO-591](https://issues.redhat.com/browse/KOGITO-591) — Use new VSCode API for WebView-based editors
* [KOGITO-622](https://issues.redhat.com/browse/KOGITO-622) Undo/Redo state control

## Chrome Extension Improvements

* [KOGITO-876](https://issues.redhat.com/browse/KOGITO-876) — Chrome Extension doesn’t work when the user is not logged in
* [KOGITO-930](https://issues.redhat.com/browse/KOGITO-930) Write unit tests for Chrome Extension components

## API Improvements

* [KOGITO-622](https://issues.redhat.com/browse/KOGITO-622) Undo/Redo state control
* [KOGITO-652](https://issues.redhat.com/browse/KOGITO-652) — Provide environment context for Kogito editors
* [KOGITO-862](https://issues.redhat.com/browse/KOGITO-862?) Support Binary content in ResourceContent API
* [KOGITO-1219](https://issues.redhat.com/browse/KOGITO-1219) Forms — Ability to flush the form state into the model on demand

Huge thanks for everyone involved in this release ;) ! 💖
