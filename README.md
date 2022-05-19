# SCSS Language Improvements (Fix the missing colors in CSS/SCSS attributes)

This extension attempts to fix the SCSS related syntax highlighting issue as described [here](https://github.com/atom/language-sass/issues/226#issuecomment-1129938430). The original extension is no longer found in VSCode market because [we thought the issue has been fixed](https://github.com/cssinate/scss-language-improvements/issues/3#issuecomment-1129960092). Because the original maintainer is not doing SCSS daily any longer, I'm keeping this project alive while waiting for the issue to be fixed (I'm not holding my breath as the previous fix took years).

## Usage

1. Install the extension from [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ronilaukkarinen.scss-language-improvements)
2. Add the following to your settings.json:

```json
"editor.tokenColorCustomizations": {
  "textMateRules": [
    {        
      "scope": "meta.property-name-custom-unique.scss",
      "settings": {
        "foreground": "#66d9ef",
      }
    },
  ]
},
```

Use the color from your color theme. This ensures the missing colors are always correct. This example is in line with my [vscode-settings](https://github.com/ronilaukkarinen/vscode-settings).

## The issue

Have you ever noticed that some properties in your SCSS files are oddly-colored by your syntax highlighter?

![screely-1652946897665](https://user-images.githubusercontent.com/1534150/169242570-6e9042a3-ac20-466a-81d8-c400c35de1a8.png)

This small extension solves that issue.

## Why does this happen in the first place?

The words `content`, `cursor`, `filter`, `font`,and `mask` are all words that have been identified as [selectors](https://github.com/atom/language-css/blob/master/grammars/css.cson#L2056) and [property names](https://github.com/atom/language-css/blob/master/grammars/css.cson#L1488).

## Why isn't this in the real language pack?

VSCode takes its SASS language definition directionly from the Atom language definition. There is an issue [here](https://github.com/atom/language-sass/issues/226) about the matter.

## How does it work?

This code change targets specifically those problematic words. This plugin first considers them property names by default, but once they're followed by a curly brace, pseudo-element or pseudo-selector, they resolve to selectors.
