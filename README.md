[![npm version](https://badge.fury.io/js/autoimport-ngtemplate-loader.svg)](https://badge.fury.io/js/autoimport-ngtemplate-loader)

# autoimport-ngtemplate-loader
Auto require AngularJS 1.x templates in Webpack style

## Usage

Install the package by running `npm install autoimport-ngtemplate-loader`. Once installed, you can add it to your Webpack config.

```js
module.exports = {
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: ['babel-loader', 'other-loaders', 'autoimport-ngtemplate-loader']
            }
        ]
    }
};
```

**Note** - It is recommended that this loader be run before any transpilation happens so it can operate on unchanged source code.

The next step is to add `ngtemplate-loader` and a loader that you want to handle your template code with. The most common one is `html-loader`. This will run every time Webpack encounters `require('something.html')`.

```js
module.exports = {
    module: {
        rules: [
            {
                test: /\.html$/,
                exclude: /node_modules/,
                use: [
                    {
                        loader: 'ngtemplate-loader',
                        options: {
                            relativeTo: 'src/'
                        }
                    },
                    {
                        loader: 'html-loader'
                    }
                ]
            }
        ]
    }
}
```

It is a good idea to add the `relativeTo` option for `ngtemplate-loader` so that the templates aren't put into the Angular template cache with absolute paths which contain platform specific or user specific information. This will affect the portability of the bundled code.

### Options

This module supports configuration through either the `options` object method or the query string method. The valid options are listed in the table below.

| Name           | Type     | Default Value                  | Details                                                                                                                      |
|----------------|----------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| `variableName` | `string` | `autoImportNgTemplateLoaderTemplate` | The variable name that gets injected into the compiled code. This is included so that variable collisions can be prevented.  |

## Development

### Installation

Once the repository is cloned, run `npm install` to get all the dependencies. The examples in this package also depend on `ngtemplate-loader` and `html-loader`. Those are declared as peer dependencies of this package so they need to be installed with `npm install ngtemplate-loader html-loader`.

If you're using a npm v5, you will need to include the `--no-save` flag so that they don't get added to the package dependencies.

### Running

There are two example projects includes. One that has one directive and another that has more. You can run `npm run one-directive`, `npm run many-directives` or `npm run multiple-directives` to see the loader in action. Once successful, examining the `build/bundle.js` file will show the results.

### Testing

The tests for this package are written in with ava. They can be run by running `npm test`.

### Linting

This project uses ESLint. All the requisite files can be linted using `npm run linter`. The rules for this project are located in `eslintrc.json`.

### Miscellaneous

This project also includes an `.nvmrc`. This is to tell [`nvm`](https://github.com/creationix/nvm) what version of Node.js to use for this project. It is set to v6.10.3 which is the current LTS release. However, any Node.js version greater than v6.10.3 should also work.

The project is also compatible with [`yarn`](https://yarnpkg.com/), Facebook's package manager. Normal `yarn` commands apply.

## Resources

* [How to write a Webpack loader](https://webpack.js.org/development/how-to-write-a-loader/)
* [Webpack Loader API](https://webpack.js.org/api/loaders/)
* [How to write a Webpack plugin](https://webpack.js.org/development/how-to-write-a-plugin/)
* [Webpack Plugin API](https://webpack.js.org/api/plugins/)
