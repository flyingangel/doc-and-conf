# Using webpack and React

> npm i webpack --save-dev  
> npm i webpack-cli --save-dev  
> npm i babel-loader babel-core babel-preset-env babel-preset-react --save-dev  
> npm i react react-dom --save-dev  
> npm i prop-types --save-dev  
> npm i html-webpack-plugin html-loader --save-dev  
> npm i webpack-dev-server --save-dev  
> mkdir -p src/js/components/{container,presentational}  


Setup file `package.json`

    "scripts": {
      "build": "webpack --mode production"
    }
    
Setup file `.babelrc`

    {
      "presets": ["env", "react"]
    }
    
Setup file `webpack.config.js`

    module.exports = {
      module: {
        rules: [
          {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
              loader: "babel-loader"
            }
          }
        ]
      }
    };

https://www.valentinog.com/blog/react-webpack-babel/
