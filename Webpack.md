# Webpack

## Overview

- basically packaging all files required for front end rendering into a single dist folder
- to do that, all files for the front end shld be in a src folder i.e.:
  - .html
  - .scss (syntatically awesome style sheets -> souped up css file )
  - js script file(s)
    - there shld be a single entry point script file conventionally named index.js
    - other script files can be imported into index.js as needed
    - importing other files/ modules into a js script is not poss w/o using webpack
    - cos not supported by browser engines? (not sure if this is the correct term)
    - w/o webpack, using multiple js script files in a single html file done thru using script tags for ea script file
  - public folder w all related assets
- files that dun need to be in the src folder are those related to the bck end i.e.:
  - config folder (w config.js for sequelize)
  - sequelize migrations, seeders & models folders
  - webpack_config folder (common, development & production config files for webpack)
  - controllers, middlewares & routers folders
  - app.mjs (or whatever express entry point for app is called)

## Some Specifics

1. script shortcuts in package.json
   - in example below:
   - npm run build will compile production mode files in dist
   - npm run watch will compile development files in dist; this shld be run using a separate terminal window cos dist files will be auto updated whenever there is change in src files
   - from RA: By default, Heroku looks for Node scripts called build and start to execute Node applications deployed to Heroku.

```code within package.json
"scripts": {
    "build": "webpack --config webpack_conf/webpack.prod.js",
    "debug": "nodemon --inspect index.mjs",
    "start": "node index.mjs",
    "watch": "webpack --watch --config webpack_conf/webpack.dev.js"
  }
```

2. webpack files split into 3. sample codes here taken from [RA's webpack-mvc-base-bootcamp main branch repo](https://github.com/rocketacademy/webpack-mvc-base-bootcamp)

   - webpack.common.js -> config common across both development and production mode
   - webpack.dev.js -> config specific to development mode
   - webpack.prod.js -> config specific to production mode

3. webpack.common.js
   - sass-loader converts scss to css
   - css-loader converts css to javascript
   - MiniCssExtractPlugin creates a .css file in dist
   - entry file specifications in dev and prod config files
   - [contenthash] is webpack's built-in way of adding a unqiue hash based on contents of file ([link here](https://webpack.js.org/guides/caching/))

```webpack.common.js
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const path = require('path');

module.exports = {
  plugins: [
    new MiniCssExtractPlugin(),
  ],
  output: {
    filename: '[name]-[contenthash].bundle.js',
    path: path.resolve(__dirname, '../dist'),
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          MiniCssExtractPlugin.loader,
          {
            loader: 'css-loader',
          },
          'sass-loader',
        ],
      },
    ],
  },
};
```

4. webpack.dev.js
   - HtmlWebpackPlugin is for moving main.html from src to dist. Want this cos we are constantly changing [name]-[contenthash].bundle.js when we are updating src files. using this plugin, webpack shld auto update script tag with the most updated src filename
   - think merge import is to be able to merge webpack.common.js with webpack.dev.js
   - common refers to webpack.common.js
   - babel used for transforming javascript from ES6 to ES5 syntax => so code can be deployed in more widely-compatible ES5 syntax ([RA: 6.1.3: Webpack with Babel](https://bootcamp.rocketacademy.co/6-frontend-infrastructure/6.1-webpack/6.1.3-webpack-with-babel))
     - @babel/preset-env: Determines how much transpiling of our code needs to be done based on other packages that it uses (e.g, compat-table, browserslist etc), i.e, how far back we need to go
     - @babel/preset-react: facilitate working with react
   - devtool setting is to create a sourceMappingURL? -> cos used "inline-source-map", this can be seen right at the end of the generated main-[hash].bundle.js file, think if use "source-map" then the sourceMappingURL will be generated in a separate file ([Source Maps - SurviveJS](https://survivejs.com/webpack/building/source-maps/))

```webpack.dev.js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  entry: {
    main: './src/index.js',
  },
  mode: 'development',
  devtool: 'inline-source-map',
  watch: true,
  module: {
    rules: [
      {
        test: /\.(js|mjs|jsx)$/, // regex to see which files to run babel on
        exclude: /node_modules/,
        use: {
          loader: require.resolve('babel-loader'),
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      // name this file main, so that it does not get automatically requested as a static file
      filename: './main.html',
      template: path.resolve(__dirname, '..', 'src', 'main.html'),
    }),

  ].filter(Boolean),
});
```

1. webpack.prod.js
   - difference w webpack.dev.js:
     - mode is production rather than development
     - `devtool` setting dropped
     - HtmlWebpackPlugin has additional setting of `inject: true` and `alwaysWriteToDisk: true`
     - babel loader settings are different there, but think is cos just not updated...

```webpack.prod.js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');
const { merge } = require('webpack-merge');
const common = require('./webpack.common.js');

module.exports = merge(common, {
  entry: {
    main: './src/index.js',
  },
  mode: 'production',
  plugins: [
    new HtmlWebpackPlugin({
      // name this file main, so that it does not get automatically requested as a static file
      filename: 'main.html',
      inject: true,
      template: path.resolve(__dirname, '..', 'src', 'main.html'),
      // a favicon can be included in the head. use this config to point to it
      // favicon: resolve(__dirname, '..', 'src', 'favicon.png'),
      alwaysWriteToDisk: true,
    }),
  ],
  module: {
    rules: [
      {
        test: /\.(js|mjs|jsx)$/, // regex to see which files to run babel on
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
    ],
  },
});
```

## Using Express and Webpack

- need 2 terminal windows
  - one to run nodemon index.mjs to reload Express app on changes in backend files
  - the other to for npm run watch, so webpack will auto re-compile dist folder files when there are changes in src folder
