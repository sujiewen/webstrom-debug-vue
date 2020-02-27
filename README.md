# webstrom-debug-vue
WebStorm+Chrome调试Vue步骤


在调试时请 注意 :

在WebStorm中启动调试时，WebStorm会根据你设置的url，自动打开新的Chrome浏览器进程访问这个设置的url，而且这个浏览器页面和你平常看到的浏览器差异会比较大，看不到书签栏，也看不到你先前所装的所有插件。这是因为平常我们打开Chrome浏览器进程时，并不会添加–remote-debugging-port选项，而WebStorm无法让已经打开的Chrome实例支持调试，所以必须重新打开一个新的Chrome浏览器进程，而且不能和原来的Chrome浏览器进程使用相同的用户数据文件夹，所以它会使用一个临时的文件夹，因此当它开始调试时看到的Chrome没有任何标签，也没有任何安装的插件。我们可以在这个浏览器上登录我们的google账号，然后将所有数据同步过来，这样下次调试时所有的书签和安装的应用也就都会存在了。我们也就可以将原来浏览器的数据导出到新的文件夹，然后在WebStorm中设置Chrome的用户数据文件夹为这个新的文件夹，这样也能将所有的书签和安装的应用导过来

另外一个 注意点 :

Web项目的调试和我们平常调试Java项目，安卓项目并不同，因为我们开发Vue项目时，使用webpack-dev-server，也就是说不是WebStorm自带的Server，此时需要先启动Server(可以使用命令行 npm run dev ，也可以通过在ide的Npm Script管理器中双击启动Server)，然后才能启动调试器。 平常我们调试Java项目或者安卓项目时都是一键启动的，而调试Web项目是需要两步的，当然我们可以在配置JavaScript Debug时，添加前置步骤来简化操作步骤

WebStorm还支持调试异步代码，Web Workers和 Service Workers

如何使用WebStorm + Chrome调试Vue应用

准备环境

在chrome中安装插件 JetBrains IDE Support
创建demo项目 vue init webpack vuejs-webpack-project
修改source map
       进入项目打开config/index.js文件, 修改source map属性，从cheap-module-eval-source-map改为source-map 
       
在js函数中打好断点
使用npm install安装好所有依赖的组件
调试

编辑调试配置，新建JavaScript调试配置，名字起个jsdebug，并设置要访问的url，以及Remote url配置，如下图所示:
       
![图片](https://github.com/sujiewen/webstrom-debug-vue/blob/master/%E6%88%AA%E5%B1%8F2020-02-27%E4%B8%8B%E5%8D%884.51.23.png)

在src的Remote url处填写: webpack:///src

保存好调试配置

先启动配置的正常server（run），可以使用WebStorm npm scripts中单击工具栏start图标启动server， 也可以在命令行中执行命令npm run start启动server
再启动配置的调试server（jsdebug），单击工具栏debug乌龟图标启动，调试DebugTest，这时候会打开一个新的chrome，如下图所示 ，将要调试页面地址复制到新打开的浏览器中开始调试





