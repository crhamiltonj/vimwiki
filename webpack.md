# Webpack

## Folder Structure

    src
     |--fonts
     |--images
     |--javascript
     |--sass

## package.json

    ```json
    {
        "name": "alltheit_boilerplate",
        "version": "1.0.0",
        "main": "index.js",
        "scripts": {
            "test": "echo \"Error: no test specified\" && exit 1",
            "build": "webpack --config webpack.config.js"
        },
        "keywords": [],
        "author": "",
        "license": "ISC",
        "devDependencies": {
            "@babel/core": "^7.6.4",
            "@babel/preset-env": "^7.6.3",
            "autoprefixer": "^9.7.0",
            "babel-loader": "^8.0.6",
            "css-loader": "^3.2.0",
            "cssnano": "^4.1.10",
            "mini-css-extract-plugin": "^0.8.0",
            "postcss-loader": "^3.0.0",
            "sass": "^1.23.1",
            "sass-loader": "^8.0.0",
            "webpack": "^4.41.2",
            "webpack-cli": "^3.3.9"
        },
        "description": ""
    }
    ```

## webpack.config.js

    ```javascript
    const path = require('path')
    const MiniCssExtractPlugin = require('mini-css-extract-plugin')

    module.exports = {
    // path to the entry point.  webpack starts work from here.
    entry: './src/javascript/index.js',

    // path and filename of the result bundle.
    // webpack will bundle all javascript into this file
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },

    module: {
        rules: [
        {
            test: /\.js$/,
            exclude: /(node_modules)/,
            use: {
            loader: 'babel-loader',
            options: {
                presets: ['@babel/preset-env']
            }
            }
        },
        {
            test: /\.(sa|sc|c)ss$/,
            use: [
            {
                loader: MiniCssExtractPlugin.loader
            },
            {
                loader: "css-loader",

            },
            {
                loader: "postcss-loader"
            },
            {
                loader: "sass-loader",
                options: {
                implementation: require("sass")
                }
            }
            ]
        }
        ]
    },
    plugins: [
        new MiniCssExtractPlugin({
        filename: 'bundle.css'
        })
    ],

    // Default mode for webpack is production
    // depending on mode webpack will apply different things
    // on a final bundle. for now we don't need production's
    // javascript minifying and other things so set the mode to development
    mode: 'development'

    }
    ```
