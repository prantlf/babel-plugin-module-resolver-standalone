# babel-plugin-module-resolver-standalone

[![Latest version](https://img.shields.io/npm/v/babel-plugin-imodule-resolver-standalone)
 ![Dependency status](https://img.shields.io/librariesio/release/npm/babel-plugin-module-resolver-standalone)
](https://www.npmjs.com/package/babel-plugin-module-resolver-standalone)

A [Babel] plugin to add a new resolver for your modules when compiling your code using Babel. This plugin allows you to transform the path of each source module using a custom JavaScript function.

This plugin can be used instead of [babel-plugin-module-resolver], if the target environment is a web browser using [@babel/standalone], with which the original plugin does not work. This plugin supports only the method [resolvePath] for the time being.

### Table of Contents

- [Installation](#installation-and-getting-started)
- [Babel Configuration Examples](#babel-configuration-examples)
- [Contributing](#contributing)
- [License](#license)

## Installation

This module can be installed in your project using [NPM], [PNPM or [Yarn]. Make sure, that you use [Node.js] version 6 or newer.

```sh
npm i -D babel-plugin-module-resolver-standalone
pnpm i -D babel-plugin-module-resolver-standalone
yarn add babel-plugin-module-resolver-standalone
```

## Babel Configuration Examples

Prepend path to utility modules to be able to import them from `utils/...` without always providing the actual full path:

```js
{
  plugins: [
    [
      'module-resolver',
      {
        resolvePath: function (sourcePath, currentFile, opts) {
          if (sourcePath.startsWith('utils/')) {
            return '../../'+ sourcePath
          }
        }
      }
    ]
  ]
}
```

Ensure, that all JavaScript module paths are prefixed by `es6!`, so that [requirejs-babel] will be applied by [RequireJS] to nested modules too:

```js
{
  plugins: [
    'transform-modules-amd',
    [
      'module-resolver',
      {
        resolvePath: function (sourcePath, currentFile, opts) {
          // Avoid prefixing modules handled by other plugins.
          if (sourcePath.indexOf('!') < 0) {
            return 'es6!' + sourcePath;
          }
        }
      }
    ]
  ]
}
```

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Lint and test your code.

## License

Copyright (c) 2019-2021 Ferdinand Prantl

Licensed under the MIT license.

[Node.js]: http://nodejs.org/
[NPM]: https://www.npmjs.com/
[PNPM]: https://pnpm.io/
[Yarn]: https://yarnpkg.com/
[RequireJS]: https://requirejs.org/
[Babel]: http://babeljs.io
[@babel/standalone]: https://github.com/babel/babel/tree/master/packages/babel-standalone
[babel-plugin-module-resolver]: https://github.com/tleunen/babel-plugin-module-resolver
[resolvePath]: https://github.com/tleunen/babel-plugin-module-resolver/blob/master/DOCS.md#resolvepath
[requirejs-babel]: https://github.com/prantlf/requirejs-babel
