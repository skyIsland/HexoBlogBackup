title: vue-cli安装以及搭建vue项目详细步骤
author: ismatch
date: 2021-10-18 09:35:50
tags:
---
> vue-cli 是vue.js的脚手架，用于快速自动生成vue.js+webpack的项目模板，这样大大降低了webpack的使用难度。下面是详细的安装步骤
- 方法/步骤
	- 第一步，检查node.js是否安装，通过命令提示符，node -v npm -v查看，如果没有请先安装node.js,如下图.
   ![image](/files/vue-cli-getstart/1.png)
	- 第二步，把npm换成cnpm，
命令行输入npm install -g cnpm --registry=https://registry.npm.taobao.org
然后cnpm -v查看版本，如下图
	![image](/files/vue-cli-getstart/2.png)
	- 第三步，全局安装webpack，
使用命令工具输入cnpm install webpack -g。
使用webpack -v查看版本
如果webpack版本4以上，需要安装webpack-cli 依赖 
使用命令工具输入cnpm install webpack webpack-cli -g 如下图
![image](/files/vue-cli-getstart/3.png)
	- 第四步，安装vue-cli
使用命令工具输入cnpm install vue-cli -g
![image](/files/vue-cli-getstart/4-1.png)
使用vue -V（这个Ｖ大写），如下图
![image](/files/vue-cli-getstart/4-2.png)
	- 第五步，上面步骤安装完后，就可以利用vue-cli初始化vue项目
在你想要安装项目的而目录下输入vue init webpack projectname（projectname是你项目的名称），
Project name:——项目名称
Project description:——项目描述
Author:——作者
Vue build:——构建模式，一般默认选择第一种
Install vue-router?:——是否安装引入vue-router，这里选是，vue-router是路由组件,后面构建项目会用到
Use ESLint to lint your code?:——这里强烈建议选no 否则你会非常痛苦，eslint的格式验证非常严格，多一个空格少一个空格都会报错，所以对于新手来说，一般不建议开启，会加大开发难度
Setup unit tests with Karma + Mocha 以及Setup e2e tests with Nightwatch这两个是测试，可以不用安装
如下图
![image](/files/vue-cli-getstart/5.png)
	- 第六步，选择上一张图片的NO,I will handle that myself（通过上下方向键来选择，按enter选中）
然后输入cd projectname(你自己取得项目名称,使用英文)
![image](/files/vue-cli-getstart/6-1.png)
然后再输入cnpm install
如下图
![image](/files/vue-cli-getstart/6-2.png)
	- 第七步，输入cnpm run dev
    ![image](/files/vue-cli-getstart/7.png)
最后在网址打开http://localhost:8080/如下图
  ![image](/files/vue-cli-getstart/7-2.jpg)
 
#### 注意事项
- 这是一个从安装到搭建的详细步骤，安装vue-cli后，新建项目从第五步开始就行了。

#### 来源：群友分享的word文档