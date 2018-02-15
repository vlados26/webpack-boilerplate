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
npm i -D webpack
npm i -D webpack-dev-server clean-webpack-plugin babel-loader babel-core babel-preset-env html-loader html-webpack-plugin sass-loader node-sass css-loader style-loader extract-text-webpack-plugin file-loader
```
