# TinyMCE Paste from Word Plugin

This plugin adds the open-source [Paste from Word](https://www.tiny.cloud/docs/plugins/opensource/paste/) functionality from the 5.x branch of TinyMCE as a plugin for the 6.x branch. The goal of this project is not to replace the premium [PowerPaste plugin](https://www.tiny.cloud/tinymce/features/powerpaste/), but to allow users who would otherwise stay on the 5.x branch solely for paste-from-word support to upgrade to later versions.

This is a fork from a previous unmaintained version of this plugin.

### Comparison with PowerPaste

| Feature                           | This Plugin | PowerPaste |
| :-------------------------------- |:-----------:|:----------:|
| Automatically cleans up content   |      ✔      |     ✔      |
| Supports embedded images          |      -      |     ✔      |
| Paste from Microsoft Word         |      ✔      |     ✔      |
| Paste from Microsoft Word online  |      ✔      |     ✔      |
| Paste from Microsoft Excel        |      -      |     ✔      |
| Paste from Microsoft Excel online |      -      |     -      |
| Paste from Google Docs            |      ✔      |     ✔      |
| Paste from Google Sheets          |      -      |     -      |

## Usage

The following instructions are for a project using ReactJS and NPM, but you can
easily modify these for any other NodeJS-based project.

1. Add the TinyMCE and TinyMCE Paste from Word Plugin projects to your package management:

```bash
npx create-react-app tinymce-react-demo
cd tinymce-react-demo
npm install --save @tinymce/tinymce-react @pangaeatech/tinymce-paste-from-word-lib
```

2. Using a text editor, open ./src/App.js and replace the contents with:

```jsx
import React from "react";
import { Editor } from "@tinymce/tinymce-react";
import PasteFromWord from "@pangaeatech/tinymce-paste-from-word-lib";

const config = {
  height: 500,
  paste_preprocess: PasteFromWord,
  paste_webkit_styles: "all",
  paste_remove_styles_if_webkit: false,
};

export default function App() {
  return (
    <Editor
      initialValue="<p>This is the initial content of the editor.</p>"
      init={config}
    />
  );
}
```

## Settings

These settings affect the execution of the `paste_from_word` plugin.

### `pastefromword_valid_elements`

This option enables you to configure the elements specific to MS Office. Word produces a lot of junk HTML, so when users paste things from Word we do extra restrictive filtering on it to remove as much of this as possible. This option enables you to specify which elements and attributes you want to include when Word contents are intercepted.

Type: String

Default Value: `"-strong/b,-em/i,-u,-span,-p,-ol,-ul,-li,-h1,-h2,-h3,-h4,-h5,-h6,-p/div,-a[href|name],sub,sup,strike,br,del,table[width],tr,td[colspan|rowspan|width],th[colspan|rowspan|width],thead,tfoot,tbody"`

### `pastefromword_convert_fake_lists`

This option lets you disable the logic that converts list like paragraph structures into real semantic HTML lists.

Type: Boolean

Default Value: `true`

### `paste_webkit_styles`

This plugin is a preprocessor which converts paste content from MS Word into WebKit-style paste content which TinyMCE's built-in paste function can handle. Therefore, it is impacted by the webkit-specific settings of the paste module. In order to prevent the paste module from stripping out all style information, you need to set this to `"all"` or to a specific list of styles you wish to retain.

Type: String

Default value: `"none"`

### `paste_remove_styles_if_webkit`

This plugin is a preprocessor which converts paste content from MS Word into WebKit-style paste content which TinyMCE's built-in paste function can handle. Therefore, it is impacted by the webkit-specific settings of the paste module. In order to prevent the paste module from stripping out all style information, you need to set this to `false`.

Type: Boolean

Default Value: `true`

## Updating package in NPM

First, make sure you

Run the following command to update the package in NPM:

```bash
npm version patch # or minor / major
npm run build
npm login
npm publish --access public
```
