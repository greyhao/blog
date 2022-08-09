## 常用命令

#### 查看版本

`npm -v`

#### 初始化

`npm init` 

`npm init -y`   跳过输入自动生成

#### 安装

`npm install `   // 安装 package.json 中配置的插件

`npm install xx `   // 安装 xx 包

install 时的一些参数

-D, --save-dev:  Package will appear in your devDependencies.

-S, --save: 保存到 package.json 



#### 卸载

`npm uninstall xx `   // 卸载某个包





### npm 和 npx 的区别

npx 是一个工具，在 npm v5.2.0 中引入的一个命令，是 npm 的一个包执行器。

npx 让 npm 包中的命令行工具和其他可执行文件在使用上变得更简单。

`npx create-react-app `   // 会把安装包 create-react-app 临时安装上，等项目初始化完成后自动删除

npx 回自动查找当前依赖包中的可执行文件，如果找不到就去环境变量里找，如果还是找不到就会安装



npx 特点：

* 临时安装可执行依赖包，不用全局安装，不用担心长期的污染
* 可以执行依赖包中的命令
* 自动加载 node_module 中的依赖包，不用指定  $PATH
* 可以指定 node 版本、命令的版本，解决不同项目使用不同版本的命令问题
