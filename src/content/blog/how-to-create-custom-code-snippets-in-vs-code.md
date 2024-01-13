---
author: Abdullah Adeel
pubDatetime: 2022-03-19T15:22:00Z
modDatetime: 2024-01-13T19:56:38Z
title: How to create custom code snippets in VS Code
slug: how-to-create-custom-code-snippets-in-vs-code
featured: true
draft: false
ogImage: /assets/blog/vscode-custom-code-snippets.webp
tags:
  - vscode
description: VS Code supports creating code snippets that come in handy to save time by not manually typing the same code again and again.
conicalUrl: https://dev.to/abdadeel/how-to-create-custom-code-snippets-in-vs-code-4e7l
---

![How to create custom code snippets in VS Code | abdadeel](@assets/blog/vscode-custom-code-snippets.webp)

## Table of contents

## Introduction

VS Code supports creating code snippets that come in handy to save time by not manually typing the same code again and again.

For example, if you're a react developer, there are concepts of components (essentially in every frontend framework - not just react). Whenever you create a new component in a separate file, you have to manually type the function and then export it from the file. And if typescript is being used, you have to define the types of `Props`.

How cool it would be to define some most used code snippets and then use them from time to time. In this article, we will see how you can build your own code snippets inside VS Code for any language of choice.

## Overview

VS Code allows you to define custom snippets in a `JSON` file format. The snippet can be global which means that you can use that snippet in any file i-e `.js`, `.java`, `.py`, `.es`, `.go`, etc. Besides that, there are dedicated files each related to a specific programming language.
Predefined files can be found by opening VS Code and going to **File > Preferences > User Snippets**.

## Creating your first snippet

In this section, we will look at how we can create a snippet for the `React` component using `typescript`. Have a look 👇.

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/42w797cj7p9uvjdmlr0l.gif)

Open VS Code and go to **Files > Preferences > User Snippets**

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3wjpc97gxkt5846evag5.PNG)

This will open VS Code pallet with options to select any language. Type `typescript` in the search bar and select **typescriptreact** option.

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/x3o8xfm50ny9xkri6m75.PNG)

This will open the `typescriptreact.json` file in your editor. This file by default contains the following content.

```js
{
  // Place your snippets for typescriptreact here. Each snippet is defined under a snippet name and has a prefix, body and
  // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
  // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the
  // same ids are connected.
  // Example:
  // "Print to console": {
  // 	"prefix": "log",
  // 	"body": [
  // 		"console.log('$1');",
  // 		"$2"
  // 	],
  // 	"description": "Log output to console"
  // }
}
```

If you have never touched this file before, this is the content you should see. Here you can already see that the comments show an example of how you can define your own snippets.

The following are required to be defined in an `Object` in order to create a custom snippet.

- **prefix** - a string or list of string that will trigger the snippet.
- **body** - a list of strings with each entry representing one line in the snippet.
- **description** - A short description that will pop up when the respective prefix is typed.

Now to add a new snippet, replace the content of your file with this 👇.

```js
{
  "Create TS React Component": {
    "prefix": "trc",
    "body": [
      "import React from 'react';",
      "",
      "interface MyComponentProps {}",
      "",
      "const MyComponent: React.FC<MyComponentProps> = (props) => {",
      "  return (",
      "    <div>",
      "      <h1>Hello World from MyComponent</h1>",
      "    </div>",
      "  );",
      "};",
      "",
      "export default MyComponent;"
    ],
    "description": "Create TS Functional React Component"
  }
}
```

This is a boilerplate for a typical react functional component using typescript. We gave it the prefix `trc` short for **_typescript react component_**. This means that as soon as we start writing `trc`, this snippet dropdown should pop up. Let's test it.

Save `typescriptreact.json` and create another file name `Button.text. You can call the file whatever you want but it should have a `.tsx` extension.

Move into that file and type **trc**. As soon as you start typing, you should see a dropdown with the first option being the best match.

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/debvwlyoj5v7igfk3f70.PNG)

Now as soon as you press enter, a new typescript react component will be create for you out of air 😉.

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tf129muq4zeug85qofka.PNG)

## Tabstops

Tabstops are the ways to modify snippet after it is created. The modification takes place by placing your cursor at the pre-specified positions. `$1`, `$2` syntax is use to represent tabstops. Read more about tabstops [here](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_tabstops).

Lets modify our snippet so that we can edit the component name as soon as it is created. Here is how you can do it.

```js
{
  "Create TS React Component": {
    "prefix": "trc",
    "body": [
      "import React from 'react';",
      "",
      "interface ${1:MyComponent}Props {}",
      "",
      "const ${1:MyComponent}: React.FC<${1:MyComponent}Props> = (props) => {",
      "  return (",
      "    <div>",
      "      <h1>Hello World from ${1:MyComponent}</h1>",
      "    </div>",
      "  );",
      "};",
      "",
      "export default ${1:MyComponent};"
    ],
    "description": "Create TS Functional React Component"
  }
}

```

Here, only one tabstop is passed and as soon as the component is created, VS Code will place multi-cursors to edit the component name if you want to. **MyComponent** after `:` is now a placeholder value. Here is the result.

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/omxgaqpr6n8dachjvnsm.PNG)

## Using Variables.

Variables can be used to add external context in your snippet. VS Code by default provide variables to use in your snippets. You can browse the full list of available variables [**here**](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variables).

Here is our example modified to by default use the filename instead of `MyComponent` as the prop.

```js
{
  "Create TS React Component": {
    "prefix": "trc",
    "body": [
      "import React from 'react';",
      "",
      "interface ${1:$TM_FILENAME_BASE}Props {}",
      "",
      "const ${1}: React.FC<${1}Props> = (props) => {",
      "  return (",
      "    <div>",
      "      <h1>Hello World from ${1}</h1>",
      "    </div>",
      "  );",
      "};",
      "",
      "export default ${1};"
    ],
    "description": "Create TS Functional React Component"
  }
}

```

![custom snippets vscode | abdadeel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lp6rivts9tgh5cfev4q3.PNG)

With that, this article concludes. If you want to get full insights on whats possible with snippets, you can visit docs here https://code.visualstudio.com/docs/editor/userdefinedsnippets.

Follow me on twitter [@abdadeel\_](https://twitter.com/abdadeel_) for more web dev and software engineering content. Thanks!
