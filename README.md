# babel-plugin-react-inline-svg

_Hint_: This is a fork of kesne's [babel-plugin-inline-react-svg](https://github.com/kesne/babel-plugin-inline-react-svg). It exists to get SVGO up to date (version 1.0.3) and enable the newest plugins.
When the original repo updates svgo, this one will probably be put down again as it only serves us for that matter.

Transforms imports to SVG files into React Components, and optimizes the SVGs with [SVGO](https://github.com/svg/svgo/).

For example, the following code...

```jsx
import React from 'react';
import CloseSVG from './close.svg';

const MyComponent = () => <CloseSvg />;
```

will be transformed into...

```jsx
import React from 'react';
const CloseSVG = () => <svg>{/* ... */}</svg>;

const MyComponent = () => <CloseSvg />;
```

## Installation

```
npm install --save-dev babel-plugin-inline-react-svg
```

## Usage

### Via `.babelrc` (Recommended)

**.babelrc**

```json
{
  "plugins": [
    "inline-react-svg"
  ]
}
```

#### Options

- *`ignorePattern`* - A pattern that imports will be tested against to selectively ignore imports.
- *`caseSensitive`* - A boolean value that if true will require file paths to match with case-sensitivity. Useful to ensure consistent behavior if working on both a case-sensitive operating system like Linux and a case-insensitive one like OS X or Windows.
- *`svgo`* - svgo options (`false` to disable). Example:
```json
{
  "plugins": [
    [
      "inline-react-svg",
      {
        "svgo": {
          "plugins": [
            {
              "removeAttrs": { "attrs": "(data-name)" }
            },
            {
              "cleanupIDs": true
            }
          ]

        }
      }
    ]
  ]
}

```

### Via CLI

```sh
$ babel --plugins inline-react-svg script.js
```

### Via Node API


```javascript
require('babel-core').transform('code', {
  plugins: ['inline-react-svg']
}) // => { code, map, ast };
```

---

Inspired by and code foundation provided by [react-svg-loader](https://github.com/boopathi/react-svg-loader).
