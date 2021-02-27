---
layout: post
title:  "What is new on Kogito Tooling from Foundation Team perspective — April/May/Jun 2020"
permalink: /:year/:month/:day/:title:output_ext
date:   2020-06-19 00:00:00 -0500
---
Recently, we had a lot of cool new features on Kogito Tooling added by Foundation Team. Those features are distributed on Kogito Tooling latest releases!
This post will do a quick overview of those. I hope you guys enjoy it!

## Visual Code Store Extension Release

Last month, the VS Code team released its custom editor as an official API, and we were finally able to publish our editors on the VS Code Store.

[![VS Code](/assets/2020/vscode.gif "VS Code")](/assets/2020/vscode.gif)


At[ Red Hat Store](https://marketplace.visualstudio.com/publishers/redhat):

* [DMN Editor](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-extension-dmn-editor) — containing DMN and SceSim;
* [BPMN Editor](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-extension-bpmn-editor);
* [Red Hat Business Automation Bundle](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-extension-red-hat-business-automation-bundle): an extension that groups all our extensions;

At[ KIE Store](https://marketplace.visualstudio.com/publishers/kie-group):

* [Kogito Bundle](https://marketplace.visualstudio.com/items?itemName=kie-group.vscode-extension-kogito-bundle): an extension that groups all our extensions for Kogito.

At this point, the bundles are just pointers to our extensions, this means that every time that you download our bundle, in fact, you are also downloading DMN and BPMN editors extensions. In the future, this bundle could potentially contain improved features, stay tuned!

See the full [post](https://medium.com/kie-foundation/we-are-on-vs-code-store-35280693573c) for details.

## Business Modeler Desktop Preview

We released a new import piece of our tool belt, the Business Modeler Desktop. This modeler is a multi-platform standalone application that enables you to quickly create and edit DMN and BPMN assets on your Desktop. See the full [blog post](https://medium.com/kie-foundation/business-modeler-desktop-preview-released-e911e78f9e11) for details.

[![Desktop](/assets/2020/desktop.gif "Desktop")](/assets/2020/desktop.gif)

## Business Modeler Hub Preview
We also released a new piece of our tooling strategy, the Business Modeler Hub Preview. A single place where you are just one click away from all our tooling channels. See the full [blog post](https://blog.kie.org/2020/05/business-modeler-hub-preview-released.html) for details.

[![Hub](/assets/2020/hub.gif "Hub")](/assets/2020/hub.gif)

## Business Modeler Preview Enhancements
We introduced some awesome UX tweaks on our Business Modeler and we expect it will improve even more your experience using it. See the full [blog post](https://medium.com/@luizjoaomotta/
business-modeler-preview-enhancements-45603f65e605) for details.

[![Preview](/assets/2020/preview.gif "Preview")](/assets/2020/preview.gif)

## Enhanced Keyboard Shortcuts On Kogito Tooling
We released a new Keyboard Shortcuts API. It gives editors the power to add custom reusable keyboard shortcuts that work in all channels! For the existing editors — BPMN, DMN and SceSim — we maintained the same mapping, but we did some under-the-hood enhancements that will make the experience even better. See the full [blog post](https://blog.kie.org/2020/05/enhanced-keyboard-shortcuts-on-kogito-tooling.html) for details.


[![Keyboard shortcuts](/assets/2020/shortcuts.gif "Preview")](/assets/2020/shortcuts.gif)

## Exporting diagrams as GitHub gists
Users can now export their DMN and BPMN diagrams as GitHub gists on the Business Modeler. See the full [blog post](https://blog.kie.org/2020/04/exporting-diagrams-as-github-gists.html) for details.

[![Gist](/assets/2020/gist.gif "Gist")](/assets/2020/gist.gif)


## Other bug fixes and improvements:

We also fixed several bugs and did some performance improvements:

### Chrome Extension

[KOGITO-1676](https://issues.redhat.com/browse/KOGITO-1676) — Chrome Extension loads editors twice

[KOGITO-1491](https://issues.redhat.com/browse/KOGITO-1491) — Sometimes editor is not loaded (Chrome extension)

[KOGITO-1725](https://issues.redhat.com/browse/KOGITO-1725) — Multiple Open in external editor links are created when the “back” button is clicked

[KOGITO-1726](https://issues.redhat.com/browse/KOGITO-1726) — Exit fullscreen on chrome extension has a different style than on the online modeler

[KOGITO-2281](https://issues.redhat.com/browse/KOGITO-2281) — Fix Chrome Extension Permissions

[KOGITO-2409](https://issues.redhat.com/browse/KOGITO-2409) — Change the name and add an icon to the chrome extension

[KOGITO-2270](https://issues.redhat.com/browse/KOGITO-2270) Update the Chrome Extension Tutorial

### Business Modeler Preview

[KOGITO-1556](https://issues.redhat.com/browse/KOGITO-1556) — DMN online editor can not be used properly in full-screen mode

[KOGITO-1782](https://issues.redhat.com/browse/KOGITO-1782) — Maximize and Minimize causes two toolbars

[KOGITO-2447](https://issues.redhat.com/browse/KOGITO-2447) — Online editor is not reflecting the URL call

[KOGITO-2354](https://issues.redhat.com/browse/KOGITO-2354) — Home page of Business Modeler Preview Online is with wrong home layout

[KOGITO-1392](https://issues.redhat.com/browse/KOGITO-1392) CSS Tweaks

[KOGITO-1461](https://issues.redhat.com/browse/KOGITO-1461) — BPMN2 Logo doesn’t show correctly

[KOGITO-1320](https://issues.redhat.com/browse/KOGITO-1320) — Prevent editors from opening with an unsupported file

[KOGITO-1668](https://issues.redhat.com/browse/KOGITO-1668) — Fix drag and drop CSS and upload button validation

[KOGITO-859](https://issues.redhat.com/browse/KOGITO-859) — Open file URL using Chrome Extension when it has CORS disabled

### Business Modeler Desktop Preview

[KOGITO-1252](https://issues.redhat.com/browse/KOGITO-1252) — Examples are not loaded correctly by desktop app

### Business Modeler Hub Preview

[KOGITO-1761](https://issues.redhat.com/browse/KOGITO-1761) — Improve error message when installing VS Code extension in a previous version of VS Code

[KOGITO-2203](https://issues.redhat.com/browse/KOGITO-2203) Non visible kebab menu

[KOGITO-1918](https://issues.redhat.com/browse/KOGITO-1918) File doesn’t save properly after tried to open an invalid one

[KOGITO-1788](https://issues.redhat.com/browse/KOGITO-1788) Desktop sort recently opened files

[KOGITO-1791](https://issues.redhat.com/browse/KOGITO-1791) CSS tweaks

### VSCode Improvements

[KOGITO-2385](https://issues.redhat.com/browse/KOGITO-2385) Adapt to new VSCode API 1.46.0

[KOGITO-2139](https://issues.redhat.com/browse/KOGITO-2139) [VSCode] “Open with…” on explorer does not work

[KOGITO-1777](https://issues.redhat.com/browse/KOGITO-1777) VSCode Store Extension Release

[KOGITO-1802](https://issues.redhat.com/browse/KOGITO-1802) Create new VSCode Extensions Distributions

[KOGITO-1778](https://issues.redhat.com/browse/KOGITO-1778) — Adapt to new VSCode API (1.44.0)

[KOGITO-1479](https://issues.redhat.com/browse/KOGITO-1479) — Upgrade Kogito VSCode extension to the final API

[KOGITO-1389](https://issues.redhat.com/browse/KOGITO-1389) — “Open to the side” not working with the newest VSCode extension (new API)

[KOGITO-1491](https://issues.redhat.com/browse/KOGITO-1491) — Sometimes editor is not loaded (Chrome extension)

[KOGITO-1863](https://issues.redhat.com/browse/KOGITO-1863) — Adapt to new VSCode API 1.45.0

[KOGITO-1837](https://issues.redhat.com/browse/KOGITO-1837) — Expose viewType and getPreviewCommandId on vscode-extension index.ts

[KOGITO-1970](https://issues.redhat.com/browse/KOGITO-1970) — Implement Undo/Redo

[KOGITO-1971](https://issues.redhat.com/browse/KOGITO-1971) — Implement SaveAs

[KOGITO-1972](https://issues.redhat.com/browse/KOGITO-1972) — Implement Revert

[KOGITO-1973](https://issues.redhat.com/browse/KOGITO-1973) — Implement async Save

[KOGITO-1974](https://issues.redhat.com/browse/KOGITO-1974) — Implement Backup

[KOGITO-1801](https://issues.redhat.com/browse/KOGITO-1801) — Dirty state of editor on consequently save operation

[KOGITO-1835](https://issues.redhat.com/browse/KOGITO-1835) — State Control API stop working on VSCode 1.44.x

[KOGITO-1034](https://issues.redhat.com/browse/KOGITO-1034) VSCode standard keyboard shortcuts don’t work while extension is enabled

[KOGITO-1748](https://issues.redhat.com/browse/KOGITO-1748) VSCode editor — Package property is empty when the process is created

[KOGITO-2128](https://issues.redhat.com/browse/KOGITO-2128) Cannot open a diagram on a new VsCode window

[KOGITO-2343](https://issues.redhat.com/browse/KOGITO-2343) Shortcuts are always active for nodes (conflict)

### Infrastructure

[KOGITO-1436](https://issues.redhat.com/browse/KOGITO-1436) — Remove double setContent call

[KOGITO-927](https://issues.redhat.com/browse/KOGITO-927) Kogito tooling CI should also build on windows

[KOGITO-1349](https://issues.redhat.com/browse/KOGITO-1349) Dev Tools — Update Patternfly to current version Editor Improvements

[KOGITO-1426](https://issues.redhat.com/browse/KOGITO-1426) Re-enable Resource Content API

## Thank you to everyone involved!

I want to thank everyone involved with this release from the awesome KIE Tooling Engineers to the lifesavers QEs and the UX people that help us look awesome!
