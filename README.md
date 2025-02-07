### ttag-po-loader
Webpack loader for Portable Object (`.po`) files for `ttag`.

A working proof of concept for https://github.com/ttag-org/ttag-webpack-plugin/issues/8

#### Installation

```console
yarn add --dev ttag-po-loader
```

#### Use
```js
import {addLocale} from "ttag";
import en_GB from "somewhere/en-GB.po";

addLocale("en-GB`", en_GB);
```

#### Webpack rules

1. Tell webpack how to load PO files

```js
config.module.rules.push({
  test: [/\.po$/],
  loader: "ttag-po-loader",
});
```

To exclude translations with the fuzzy flag, add option `excludeFuzzy` to loader:

```js
config.module.rules.push({
  test: [/\.po$/],
  loader: "ttag-po-loader",
  options: {
    excludeFuzzy: true,
  },
});
```

2. Exempt PO files from default rules if you use create-react-app

```js
const loaders = config.module.rules.find(r => r.oneOf).oneOf;
loaders.find(l => l?.loader?.match(/file-loader/)).exclude.push(/[.]po$/);
```
