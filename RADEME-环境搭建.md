# typescript 环境搭建

## 1.npm init

#### 初始化一些配置

> `{ "name": "client-side", "version": "1.0.0", "description": "source code of ts-learning", "main": "./src/index.ts", "scripts": { "test": "echo \"Error: no test specified\"} }`

## 2.创建一些文件夹

### src

- ##### utils 跟业务相关的可封装方法
- ##### tools 跟业务无关的可封装方法
- ##### assets 静态资源
- ##### api 接口方法封装
- ##### config 配置文件(需要修改的配置文件)

### typings 为 typescript 写的声明文件

### build 打包上线或本地测试的服务配置

## 3.安装依赖

- ##### npm install typescript tslint -g
- ##### tsc --init
  > ##### 用 tsc 初始化 typescript 配置文件，生成 tsconfig.json 文件
- ##### npm install webpack webpack-cli webpack-dev-server -d
  > ##### webpack-dev-server 本地开发需要的依赖
- ##### 在 build 下创建 webpack.config.js
  > ##### webpack 配置文件

## 4.运行和测试配置

- ##### 运行在 node 环境下，编译时运行
      const HtmlWebpackPlugin = require('html-webpack-plugin')
        const { CleanWebpackPlugin } = require('clean-webpack-plugin')
      module.exports = {
      entry: "./src/index.ts",
      output: {
      filename: "main.js"
      },
      resolve: {
      /**
      * 引用文件是否需要写文件类型（.js）
      */
      extensions: ['.ts', '.tsx', '.js']
      },
      module: {
      rules: [
      {
      test: /\.tsx?$/,
      use: 'ts-loader',
      exclude: /node_modules/
      }
      ]
      },
      devtool: process.env.NODE_ENV === 'production' ? false : 'inline-source-map',
      devServer: {
      contentBase: './dist',
      stats: 'errors-only',
      compress: false,
      host: 'localhost',
      port: '8089'
      },
      plugins: [
      new CleanWebpackPlugin({
      cleanOnceBaforeBuildPatterns: ['./dist']
      }),
      new HtmlWebpackPlugin({
      template: './src/template/index.html'
      })
      ]
      }
  > * entry 入口文件（本地开发或打包的入口文件） 
  > * output 编译后输出文件 
  >> * filename 文件名 
  > * resolve 
  >> * 设置自动解析的文件类型（后缀名） 
  > * module 
  >> * rules 对指定文件的处理 
  >>> * test 正则匹配（符合这个规则的文件） 
  >>> * use 处理匹配到的文件 
  >>> * exclude 排除不用处理的文件 
  > * devtool 调试时定位到代码
- ##### 在 package.json 文件的 scripts 里添加指令
  > * 创建一个 start 指令，执行 webpack-dev-server 命令，--config 指定配置文件地址，通过 cross-env 工具向配置文件传递参数，参数 key=参数 value
