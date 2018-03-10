# use-webpack
 let path = require('path');

 let htmlWebpackPlugin = require('html-webpack-plugin');

 let webpack = require('webpack');

 let CleanWebpackPlugin = require('clean-webpack-plugin');

 const ExtractTextPlugin = require("extract-text-webpack-plugin");

 module.exports={

    entry:{
    
        index:'./src/js/index.js',
        
        cart: './src/js/cart.js' 
        
    },
    
    output:{
    
       path:path.join(__dirname,'./dist'),
       
       filename: 'js/[name].js',
       
       publicPath:'' 
       
    },
    
    module:{
    
        rules:[{
        
            test: /\.css$/,
            
            include:path.join(__dirname,'src'),
            
            exclude:'/node_modules/',
            
            use: ExtractTextPlugin.extract({
            
              fallback: "style-loader",
              
              use: "css-loader"
              
            })
            
        }]
        
    },
    
    plugins: [
    
        new ExtractTextPlugin("index.css"),
        
        new CleanWebpackPlugin([
        
            './dist',
            
          ], {
            root:    path.join(__dirname,''),
            
            verbose:  true,
            
            dry:      false
            
        })
        
        ,new htmlWebpackPlugin({
        
        filename: 'index.html',
        
        template: './src/index.html',
        
        chunks:['index']
        
    }),new htmlWebpackPlugin({
    
        filename: 'cart.html',
        
        template: './src/cart.html',
        
        chunks:['cart']
        
    }),
    
    new webpack.ProvidePlugin({
    
        $:"jquery",
        
        jquery:'jquery',
        
        'window.jqery':'jquery'
        
    })
    
   ]
   
}
