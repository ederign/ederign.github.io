---
layout: post
title:  "Automatically generate BPMN/DMN SVG on VS Code"
permalink: /:year/:month/:day/:title:output_ext
date:   2021-11-03 00:00:00 -0500
fav: false
---

To provide better integration with the KIE server and Business Central, on the [Kogito Tooling 0.14 release](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-extension-bpmn-editor), we introduced a way to, on VS Code, automatically generate SVG on each save of your BPMN and DMN Diagram. Take a look at this feature in action:

[![svg1](/assets/2021/svg1.gif "svg")](/assets/2021/svg1.gif)

### How to configure it

To auto-generate on VS Code the SVG on each save of your BPMN and DMN diagrams; you need to add two properties to your user and workspace settings (settings.json, the VS Code configuration file):

```
"kogito.bpmn.runOnSave": "extension.kogito.silentlyGenerateSvgBpmn",
"kogito.dmn.runOnSave": "extension.kogito.silentlyGenerateSvgDmn",
```

To do that, open your user and workspace settings, use the following VS Code menu command:

* On Windows/Linux - File > Preferences > Settings
* On macOS - Code > Preferences > Settings

From there, access menu Extension > BPMN (or DMN), and click on 'Edit in settings.json':

[![svg2](/assets/2021/svg2.png "svg")](/assets/2021/svg2.png)

And finally, add the respective properties to the end of this file and save it:

[![svg3](/assets/2021/svg3.png "svg")](/assets/2021/svg3.png)

If you need any further questions, please let us know in the comment section!

[kie]
