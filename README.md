# <a href="https://github.com/dai-shi/es-beautifier"><img alt="logo" src="https://dai-shi.github.io/es-beautifier/images/logo2.svg" height="64" /></a>

[![Build Status](https://travis-ci.org/dai-shi/es-beautifier.svg?branch=master)](https://travis-ci.org/dai-shi/es-beautifier)
[![npm](https://img.shields.io/npm/v/es-beautifier.svg)](https://www.npmjs.com/package/es-beautifier)
[![vim](https://img.shields.io/badge/vim-available-green.svg)](https://github.com/dai-shi/es-beautifier/blob/master/contrib/vim/doc/es-beautifier.txt)
[![atom](https://img.shields.io/apm/v/es-beautifier.svg)](https://atom.io/packages/es-beautifier)
[![vscode](http://vsmarketplacebadge.apphb.com/version-short/dai-shi.vscode-es-beautifier.svg)](https://marketplace.visualstudio.com/items?itemName=dai-shi.vscode-es-beautifier)

ECMAScript beautifier based on [eslint](http://eslint.org/)

![screenshot](https://dai-shi.github.io/es-beautifier/images/screen01.png)

## Motivation

JS Beautifier is so great that it can reduce formatting issues, however,
there are two major issues: a) customization and b) ES.next.

a) If you like the result of code generated by JS Beautifier,
it's just fine, but if you can't manage with its configuration options,
you are out of luck.

b) If you are using a new ECMAScript feature or features that are not
even standardized, you are also out of luck, because the parser
does not support the features. Among such is JSX.

ESLint is a linting tool widely used, which adopts a pluggable
architecture so that it's highly customizable.
It also has an ability to automatically fix problems.
There's lots of plugins developed, forming a big ecosystem.

So, why not build a beautifying tool using eslint?

## Usage (CLI)

### Install

```
npm install es-beautifier -g --only=production
```

```
es-beautifier --help
```

### Example

```
es-beautifier < file.js > file-beautified.js
```

```
es-beautifier file-to-be-beautified.js
```

## Usage (Vim)

### Example with NeoBundle

```
NeoBundle 'dai-shi/es-beautifier', {'rtp': 'contrib/vim', 'external_commands': 'node', 'build_commands': 'npm', 'build': {'others': 'npm install --only=production'}}
autocmd FileType javascript nnoremap <buffer> <Leader>e :call EsBeautifier()<cr>
autocmd FileType javascript vnoremap <buffer> <Leader>e :call RangeEsBeautifier()<cr>
```

## Usage (Atom)

<https://atom.io/packages/es-beautifier>

Toggle the Command Palette and enter "es-beautifier".

For the long term use, you might want to configure keybindings, for example:
```
'atom-text-editor':
  'shift-cmd-e': 'es-beautifier'
```

## Usage (Visual Studio Code)

```
ext install vscode-es-beautifier
```

Open the Change Language Mode (Cmd-K M / Ctrl-K M) and select "es-beautifier".
You can format code just like the original formatter.

For the long term use, you might want to configure it in `settings.json`:
```
{
  "files.associations": {"*.js":"es-beautifier"}
}
```

## Usage (eslint-plugin)

You can customize it just like a normal eslint plugin.

### Install

In your project directory:

```
npm install eslint eslint-plugin-es-beautifier --save-dev
```

### Example

Add the following to your `.eslintrc` or `eslintConfig` in package.json.

```
{
  "plugins": [
    "es-beautifier"
  ],
  "extends": [
    "plugin:es-beautifier/standard"
  ]
}
```

Add the following `scripts` in package.json.

```
{
  "scripts": {
    "beautify": "eslint --fix ."
  }
}
```

Run:

```
npm run beautify
```

## Similar projects

There are several tools that do smiliar to what es-beautifier does.

- [js-beautify](https://github.com/beautify-web/js-beautify)
- [uglify-js](https://github.com/mishoo/UglifyJS2)
- [esformatter](https://github.com/millermedeiros/esformatter)
- [prettydiff](https://github.com/prettydiff/prettydiff)

To see the comparison:

```
git clone https://github.com/dai-shi/es-beautifier.git
cd es-beautifier
npm install
npm run examples
```

Here's more intuitive (biased) comparison in table:

|                | js-beautify | uglify-js | esformatter | prettydiff | es-beautifier |
|----------------|-------------|-----------|-------------|------------|---------------|
| ES2015 Parser  | Own         | Own       | Esprima     | Own        | Espree         |
| Customization  | Limited     | No        | Plugin      | Somewhat   | Plugin        |
| Comments       | OK          | Removed   | OK          | OK         | OK            |
| JSX Support    | No          | Error     | No          | Limited    | Yes           |
| Array in array | Yes         | No        | No          | Wierd      | Yes           |
| Execution Time | Short       | Short     | Long        | Short      | Long          |
| Completion     | Mature      | Good      | Young       | Good       | Young         |

## Blogs

- [ECMAScript beautifier based on eslint](https://medium.com/@dai_shi/ecmascript-beautifier-based-on-eslint-2e2005dda955)
