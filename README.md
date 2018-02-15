# Webpack 3 Boilerplate for beginners
A basic webpack 3 boilerplate for beginners to start with any JS/ES6 based project.
<br>
## Guide
This basic boilerplate is the final output of this comprehensive write up on Medium. I recommend to read this article to know the insight of how you can configure webpack from scratch.
[Webpack 3 quickstarter: Configure webpack from scratch](https://medium.com/@nirjhor123/webpack-3-quickstarter-configure-webpack-from-scratch-30a6c394038a)
<br>
## Install dependencies

```
npm install
```


## Develop locally with webpack-dev-server
1. Run

```
npm run dev
```

2. In your browser, navigate to: [http://localhost:2000/](http://localhost:2000/)
## For bundled output

```
npm run build
```

## For production-ready output

```
npm run build:prod
```
 
## Loaders and Plugins used in this boilerplate

### Loaders
* babel-loader
* html-loader
* sass-loader
* css-loader
* style-loader
* file-loader

### Plugins
* clean-webpack-plugin
* extract-text-webpack-plugin
* html-webpack-plugin

## Cheat-sheet

### 1. Run these commands one after another in the terminal to create project folders and install all dependencies

```
mkdir project_name && cd project_name
npm init
mkdir src dist src/assets src/assets/media src/assets/js src/assets/scss
touch webpack.config.js README.md .babelrc src/index.html src/app.js src/assets/scss/app.scss
npm i -D webpack webpack-dev-server  
npm i -D clean-webpack-plugin babel-loader babel-core babel-preset-env 
npm i -D html-loader html-webpack-plugin sass-loader node-sass css-loader style-loader  
npm i -D extract-text-webpack-plugin file-loader
```

### 2. Add this snippet into .babelrc

```
{
  "presets": ["env"]
}
```

### 3. Configure package.json > scripts with this snippet

```
"scripts": {
  "build": "./node_modules/.bin/webpack",
  "build:prod": "./node_modules/.bin/webpack -p",
  "watch": "./node_modules/.bin/webpack --watch",
  "dev": "./node_modules/.bin/webpack-dev-server"
}
```

### 4. Import app.scss into your app.js

```
import './assets/scss/app.scss';
```

### 5. Populate your src/index.html (with an image too) and src/assets/scss/app.scss and add the image into src/assets/media

### 6. Copy and paste this configuration file into your webpack.config.js (make sure that project folders hierarchy to be same)

```
const path = require('path'),
      webpack = require('webpack'),
      CleanWebpackPlugin = require('clean-webpack-plugin'),
      HtmlWebpackPlugin = require('html-webpack-plugin'),
      ExtractTextPlugin = require('extract-text-webpack-plugin');

const extractPlugin = new ExtractTextPlugin({ filename: './assets/css/app.css' });

const config = {

  // absolute path for project root with the 'src' folder
  context: path.resolve(__dirname, 'src'),

  entry: {
    // relative path declaration
    app: './app.js'
  },

  output: {
    // absolute path declaration
    path: path.resolve(__dirname, 'dist'),
    filename: './assets/js/[name].bundle.js'
  },

  module: {
    rules: [

      // babel-loader with 'env' preset
      { test: /\.js$/, include: /src/, exclude: /node_modules/, use: { loader: "babel-loader", options: { presets: ['env'] } } },
      // html-loader
      { test: /\.html$/, use: ['html-loader'] },
      // sass-loader with sourceMap activated
      {
        test: /\.scss$/,
        include: [path.resolve(__dirname, 'src', 'assets', 'scss')],
        use: extractPlugin.extract({
          use: [
            {
              loader: 'css-loader',
              options: {
                sourceMap: true
              }
            },
            {
              loader: 'sass-loader',
              options: {
                sourceMap: true
              }
            }
          ],
          fallback: 'style-loader'
        })
      },
      // file-loader(for images)
      { test: /\.(jpg|png|gif|svg)$/, use: [ { loader: 'file-loader', options: { name: '[name].[ext]', outputPath: './assets/media/' } } ] },
      // file-loader(for fonts)
      { test: /\.(woff|woff2|eot|ttf|otf)$/, use: ['file-loader'] }

    ]
  },

  plugins: [
    // cleaning up only 'dist' folder
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin({
      template: 'index.html'
    }),
    // extract-text-webpack-plugin instance
    extractPlugin
  ],

  devServer: {
    // static files served from here
    contentBase: path.resolve(__dirname, "./dist/assets/media"),
    compress: true,
    // open app in localhost:2000
    port: 2000,
    stats: 'errors-only',
    open: true
  },

  devtool: 'inline-source-map'

};

module.exports = config;
```
