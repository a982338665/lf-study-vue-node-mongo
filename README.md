# vue-node-mongo
mall

### 1.基于MV*模式的VUE框架
    
    ·model绑定view
    ·没有控制器概念
    ·数据驱动，状态管理
    
### 2.全栈开发简易商城：vue+node+mongo（vue-cli webpack）

#### 2.1 前置知识
    
    1.html/css/js
    2.vue
    3.es6
    4.node
    5.npm 
    6.webpack
   
#### 2.2 vue基础：

##### 2.2.1 nodejs和npm的安装和环境搭建
    
    ·cnpm list
    ·npm list
    
##### 2.2.2 vue环境搭建及vue-cli的使用
    
    1.vue多页面应用文件引入：D:\go-20191030\vue-node-mongo\demo1\index.html
        ·官网拷贝：... 、使用 CDN 方法
            以下推荐国外比较稳定的两个 CDN，国内还没发现哪一家比较好，目前还是建议下载到本地。
            Staticfile CDN（国内） : https://cdn.staticfile.org/vue/2.2.2/vue.min.js
            unpkg：https://unpkg.com/vue/dist/vue.js, 会保持和 npm 发布的最新的版本一致。
            cdnjs : https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js
        ·npm安装：D:\go-20191030\vue-node-mongo\demo2
            cnpm i vue --save   安装vue并且，添加到package.json里
    2.vue-cli构建SPA应用：-- 安装脚手架
        1.安装：npm install -g vue-cli
        2.初始化项目-简单模式的webpack项目：vue init webpack-simple demo3 [vue-node-mongo下执行] D:\go-20191030\vue-node-mongo\demo3
        3.初始化项目-完整模式的webpack项目：vue init webpack demo4        [vue-node-mongo下执行] D:\go-20191030\vue-node-mongo\demo4
            ? Project name demo4
            ? Project description miaoshu
            ? Author li
            ? Vue build standalone
            ? Install vue-router? Yes              项目路由
            ? Use ESLint to lint your code? No     代码检查 
            ? Set up unit tests No                 单元测试 
            ? Setup e2e tests with Nightwatch? No

##### 2.2.3 vue配置介绍：主要关注
    
    1.D:\go-20191030\vue-node-mongo\demo4\config\index.js
    2.D:\go-20191030\vue-node-mongo\demo4\build\webpack.base.conf.js
    
##### 2.2.4 vue基础语法
    
    1.模板语法：
        ·Mustache语法：{{msg}}
        ·Html赋值：v-html=""
        ·绑定属性：v-bind:id=""
        ·文本赋值：v-text=""
        ·使用表达式：{{ok?'yes':'no'}}
        ·if：v-if=""
        ·过滤器：{{message|capitalize}} 和v-bind:id = 'rawId | formatId'
    2.Class和Style绑定:
        ·对象语法：v-bind:class="{active:isActive}" isActive是data中的值，通过此来判断属性是否该显示
        ·数组语法：
        ·style绑定：v-bind:style="{color:colorVal}" colorVal是data中的值，通过此来判断属性是否该显示
    3.条件渲染：
        ·v-if
        ·v-else
        ·v-else-if
        ·v-show     判断div是否显示或隐藏
        ·v-cloak    
    4.事件处理器：
        ·v-on:click="greet" 或者 @click ="greet"
        ·v-on:click.stop            阻止冒泡
        ·v-on:click.stop.prevent    阻止默认事件，例如a标签，点击会跳转，该属性会阻止该事件
        ·v-on:click.self            给div事件绑定
        ·v-on:click.once            给事件绑定一次，仅生效一次
        ·v-on:keyup.enter           键盘事件
            tab
            delete
            esc
            space
            up
            down
            left
            right
    5.vue组件：
        ·全局和局部组件
        ·父子组件通信 -数据传递 prop emit 只允许父组件流向子组件，通过emit可以变相将子组件数据流向父组件
        ·slot

#### 2.3 vue路由：vue-router

    1.vue-router用来构建SPA
    2.<router-link></router-link>或者this.$router.push({path:''}) 跳转实为a标签
    3.<router-view></router-view>   组件渲染 和2配合使用
    4.路由介绍：
        ·动态路由匹配
            模式              匹配路径            $route.params
            /user/:username  /user/evan         {username:'evan'}
            /user/:a1/a2     /user/1/2          {a1:'1',a2:'2'}
        ·嵌套路由: html里面的路由
        ·编程式路由：通过js实现页面跳转
            $router.push('name')
            $router.push({path:'name'})
            $router.push({path:'name?a=13'})
            $router.push({path:'name',query:{a:123}})
            $router.go(1) 和go(-1)  
        ·命名路由和命名视图
            ·给路由定义不同的名字，根据名字进行匹配    
            ·给不同的route-view定义名字，通过名字进行对应组件的渲染
 
#### 2.4 vue-resources和Axios：

    1.使用：
        cdn
        npm安装
    2.vue-resource的请求api是按照rest风格设计的：
        get head post 等
    3.基础介绍：
        url             string              路径
        method          string              请求方式
        body            obj,formdatastring  请求体
        params          obj                 url参数
        headers         obj                 请求头
        timeout         number              超时时间
        before          function(request)   请求发送前的处理函数，类似于jquery的beforeSend函数
        progress        function(event)     ProgressEvent的回调函数
        credientials    bool                表示跨域请求时是否需要使用凭证
        emulateHttp     bool                f发送put，pathch，delete请求时以http post请求方式方法，并设置请求头的x-http-method-override
    4.全局拦截器interceptors
        Vue.http.interceptors.push((request,next)=>{
            //请求发送前的处理逻辑
            next((response)=>{
                //请求发送后的处理逻辑
                //根据请求状态，response参数会返回给successCallback或errorCallback
                return response;
            });
        })
    5.使用：demo4
        npm i vue-resource --save [--save添加至生产依赖中] D:\go-20191030\vue-node-mongo\demo4\vue-resource.html
    6.Axios：异步型插件 D:\go-20191030\vue-node-mongo\demo4\vue-axios.html
        1.引入：
            cdn引入：
            npm i axios --save
        2.使用：

#### 2.5 ES6语法：

##### 2.5.1 简介
    
    1.1995 js诞生
    2.1996 ES标准确立【国际化】
    3.2009 ES5出现
    4.2015 ES2015 简称ES6出现
    5.目标：使用js来编写复杂的大型应用程序，成为企业级开发语言
    
##### 2.5.2 常用命令
    
    1.let和const命令
    2.模板语言
    3.字符串，对象，数组和函数的解构
    4.Rest参数和函数的扩展
    5.箭头函数
    6.Promise函数：避免回调地狱
    7.模块化开发 export import:import可以实现异步加载 --》 在方法内引用import
    
##### 2.5.3 AMD,CMD,Commonjs和ES6的对比
    
    1.AMD - ajax model define异步模块定义：是RequreJS在推广过程中对模块定义的规范化产出，依赖前置，需要时引入，异步加载
        //第一个参数引入包，第二个参数，通过回调获取包
        define(['package/lib'],function(lib){
            function foo(){
                lib.log('hello world')
            }
            return {
                foo:foo
            }
        })
    2.CMD -同步模块定义：是SeaJS在推广过程中对模块定义的规范化产出,哪个地方用哪个地方引入
        //所有模块都通过define来定义
        define(function(require,exports,module){
            //通过require引入依赖
            var $ =require('jquery')
        })
    3.CommonJS规范 - module.exports nodejs支持，浏览器端不支持
        exports.sum = (x,y) => x + y;
    4.ES6特性新增 export/import

#### 2.6 商品列表模块实现：

    1.基础组件拆分：
        Header组件
        Footer组件
        面包屑组件
    2.项目初始化：
        1.vue init webpack simple-mall 
          author: foluojack
        2.cd simple-mall
        3.npm install
        4.npm run dev
        5.npm i axios --save
        6.cnpm i vue-lazyload --save
    3.改造：
        1.src/assets中存放的静态文件：主要用于在组件中引用的内容，会在打包时，打进去
        2.static文件夹中的静态文件不会被打包进去，放一些比较大的图片之类的
        -----
        3.将html中body的内容粘贴到views文件夹下的vue文件中
        4.将引用的css粘贴到src/assets/css中,将img内容粘贴到static文件夹中
        5.在GoodsList.vue文件中引用css，并将图片引用路径修改为 static/...
        6.修改index.js,使用组件
        
        7.商品列表数据渲染实现
            ·模拟假数据mock数据，加载商品列表信息
            1.新建文件夹mock，写入假数据
            2.使用axios模拟请求
        8.实现图片懒加载：
            1.cnpm i vue-lazyload --save
            2.主要用于，图片滚动时，未滚动到图片时，不进行图片加载，避免一时间大量加载图片耗费资源

#### 2.7 nodejs：
    
    1.安装nodejs
    2.创建httpserver
    3.node加载静态资源
    4.express框架：
        cnpm i -g express-generator
        cd simple-mall-api
        express -e （将当前目录作为express初始化项目）
        npm install
        
#### 2.8 mongodb介绍：
    
    1.安装，用户创建，基本语法
    2.数据表设计：
    3.启动mongo
    4.初始化数据：
        D:\go-20191030\vue-node-mongo\simple-mall\resource\dumall-goods
        D:\go-20191030\vue-node-mongo\simple-mall\resource\dumall-users

#### 2.9 node开发商品列表接口
    
    1.node调试方式：
        1.idea直接run
        2.pm2：基于进程管理，不能跨电脑，也就是后台运行
            cnpm i pm2 -g
            pm2 start bin/www
            pm2 stop bin/www
            pm2 stop all 停止所有
    2.实现商品列表查询接口：
        1.安装mongoose：
            cnpm i mongoose --save
        2.创建model
        3.创建路由
        4.基于mongoose，实现查询功能
    3.前端页面分页排序：
        1.分页插件：vue-infinite-scroll,具体使用api可以去npm查询
            cnpm i vue-infinite-scroll --save
    4.商品价格过滤功能
    5.加入购物车
    
 #### 2.10 登录模块实现：
    
    1.登入
    2.登出
    3.拦截未登录用户
    4.全局模态框组件实现:弹框组件化
    
#### 2.11 购物车模块实现：
    
    1.
