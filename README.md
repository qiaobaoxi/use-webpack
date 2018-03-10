# use-webpack
    let path = require('path');

    let htmlWebpackPlugin = require('html-webpack-plugin');

    let webpack = require('webpack');

    let CleanWebpackPlugin = require('clean-webpack-plugin');

    const ExtractTextPlugin = require("extract-text-webpack-plugin");

    module.exports={

    entry:{
    
        index:'./src/js/index.js',入口文件
        
        cart: './src/js/cart.js' 入口文件
        
    },
    
    output:{
    
       path:path.join(__dirname,'./dist'),输出文件地址
       
       filename: 'js/[name].js',//输出文件
       
       publicPath:'' //前缀比如加cdn地址
       
    },
    
    module:{
    
        rules:[{
        
            test: /\.css$/,匹配对象
            
            include:path.join(__dirname,'src'),编译区域
            
            exclude:'/node_modules/',不编译区域
           
            use: ExtractTextPlugin.extract({解析css-loader
            
              fallback: "style-loader",
              
              use: "css-loader"
              
            })
            
        }]
        
    },
    
    plugins: [
    
        new ExtractTextPlugin("index.css"),//抽取文本
        
        new CleanWebpackPlugin([//清除文件插件
           
            './dist',
            
          ], {
            root:    path.join(__dirname,''),
            
            verbose:  true,
            
            dry:      false
            
        })
        
        ,new htmlWebpackPlugin({生成html
        
        filename: 'index.html',
        
        template: './src/index.html',
        
        chunks:['index']由于多个js要引入某个js chunk
        
    }),new htmlWebpackPlugin({
    
        filename: 'cart.html',
        
        template: './src/cart.html',
        
        chunks:['cart']
        
    }),
    
    new webpack.ProvidePlugin({引入第三方插件
    
        $:"jquery",
        
        jquery:'jquery',
        
        'window.jqery':'jquery'
        
    })
    
    ]
   
  }
