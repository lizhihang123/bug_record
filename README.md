>这份文件，记录了我预见的错误，以及对应的解决方法。
>
>我觉得碰到错误时，回想以前是否碰到过这个错误，如果有记录解决方式，那将会省掉很多力气。不然又要去csdn，又要去接受新的知识点，会很辛苦
>但是之前记录的方式有点不太对。最好的情况是，在“什么样的情况下”，遇见了“什么报错”，怎么解决的。这样是最好的，慢慢改善起来

# 1. 引入组件



```javascript
Already included file name 'd:/黑马程序员/VUE第五阶段/webpack+Vue基础课程资料/Day04_vue组件_组件通信_todo案例/02_代码/vuecomponent2/demmo/src/components/Pannel.vue' differs from file name 'd:/黑马程序员/VUE第五阶段/webpack+Vue基础课程资料/Day04_vue组件_组件通信_todo案例/02_代码/vuecomponent2/demmo/src/components/pannel.vue' only in casing.
  // The file is in the program because:
    Imported via "./components/Pannel.vue" from file 'd:/黑马程序员/VUE第五阶段/webpack+Vue基础课程资料/Day04_vue组件_组件通信_todo案例/02_代码/vuecomponent2/demmo/src/App.vue'
    Root file specified for compilation
```



修改： 后缀.vue去掉







有时又会自动加上后缀



# 2. 报错 vue-plugin-vue



前提，记得配置好

vue.config.js里面增加属性 和 package.json同级



```javascript
module.exports = {
    devServer: {
        port: 9000,
        open: true
    },
    lintOnSave: false // 增加这句代码
}
```



其次，多复制到别的App.vue文件看看报不报错，百度好多方案都很水，或者我没读懂那些



# 3. create hook拼写错误



## 3.1  创建生命周期函数



created()才是对的

create是错的

# 4. trim方法报错



## 4.1 trim



```plain
this.age.trim() is not a function
```



如果this.age是一个数字，那么就会报错



trim去除的是字符串



解决方法：把age也改成字符串的格式



疯狂的打印值，看看是啥类型。



也有可能是this指向问题？



方法写错位置的问题？



# 5. vue方法错误



Expected Array, got String with value “”





定位页面 myFooter.vue



说明是this.arr.every找到是关键语句





如果找不到是哪个data出问题，就注释的方式



最终发现list初始化定义的是“”，但是应该改成[]，因为后续的赋值是数组



# 6. vetur.config.js



找不到package.js  或者是 ts.config.js?



```plain
https://vuejs.github.io/vetur/guide/setup.html#typescript
```



根目录创建 vetur.config.js



复制下面代码



成功，但是会不会产生啥问题呢？



```plain
// vetur.config.js
/** @type {import('vls').VeturConfig} */
module.exports = {
  // **optional** default: `{}`
  // override vscode settings
  // Notice: It only affects the settings used by Vetur.
  settings: {
    "vetur.useWorkspaceDependencies": true,
    "vetur.experimental.templateInterpolationService": true
  },
  // **optional** default: `[{ root: './' }]`
  // support monorepos
  projects: [
    './packages/repo2', // Shorthand for specifying only the project root location
    {
      // **required**
      // Where is your project?
      // It is relative to `vetur.config.js`.
      root: './packages/repo1',
      // **optional** default: `'package.json'`
      // Where is `package.json` in the project?
      // We use it to determine the version of vue.
      // It is relative to root property.
      package: './package.json',
      // **optional**
      // Where is TypeScript config file in the project?
      // It is relative to root property.
      tsconfig: './tsconfig.json',
      // **optional** default: `'./.vscode/vetur/snippets'`
      // Where is vetur custom snippets folders?
      snippetFolder: './.vscode/vetur/snippets',
      // **optional** default: `[]`
      // Register globally Vue component glob.
      // If you set it, you can get completion by that components.
      // It is relative to root property.
      // Notice: It won't actually do it. You need to use `require.context` or `Vue.component`
      globalComponents: [
        './src/components/**/*.vue'
      ]
    }
  ]
}
```



# 7. 重命名文件过快







解决方式： 重启vscode即可、



Already included file name



root file specified for compilation



# 8. sockjs.node报错



sockjs.js







```javascript
	解决方案： 
		# 找到 *node_modules*下的 
		# /node_modules/sockjs-client/dist/sockjs.js 里面的 这么一段代码
		# 大概在1608 行
		  try {
		    self.xhr.send(payload);  // 注释掉这一行
		  } catch (e) {
		    self.emit('finish', 0, '');
		    self._cleanup(false);
		  }
```



```plain
如果你的项目没有用到 sockjs，vuecli3 运行 npm run serve 之后 network 里面一直调用一个接口：http://localhost:8080/sockjs-node/info?t=1462183700002
```



# 9. vue路由重复点击报错



```plain
 Uncaught (in promise) NavigationDuplicated: Avoided redundant navigation 问题
```



https://blog.csdn.net/qq_36437172/article/details/108269846
main.js文件下，写下



```javascript
// src/router/index.js
Vue.use(Router)
const router = new Router({
  routes
})
 
const VueRouterPush = Router.prototype.push
Router.prototype.push = function push (to) {
  return VueRouterPush.call(this, to).catch(err => err)
}
```



# 10. cant’t resolve [@api ]() 



原因是复制过来的play文件夹，引入了@api这个文件，但是本地没有



# 12. vue console.log()



console.log()打印失败原因？



原因不详，但是重启谷歌浏览器默认设置，就能够恢复



# 13. yarn serve报错







vue-cli-service 不是内部或者 外部命令



或者 yarn install 下载所有依赖



# 14. 组件 动态属性之间用逗号报错











```plain
Failed to execute 'setAttribute' on 'Element' :
```



解决方法： 去掉逗号



标签里面不能写逗号



# 15.  按需导入 按需导出



```plain
Error in created hook (Promise/async): "TypeError: Object(...) is not a function"
```



```plain
出现api文件里面写了很多api 但是引入的时候这个api是undefined

export {
  导出是一个对象
}
导入 给他取一个名字
import * as visitor from '@/'
```





# 16. is not iterable



Error in v-on handler (Promise/async): "TypeError: undefined is not iterable (cannot read property Symbol(Symbol.iterator))"



函数的方法传入的参数错误



# 17. 内部命令或者外部命令



缺少包



要下包



npm install



或者yarn







# 18 camel



# bug: is not in camel case



没有使用驼峰命名法



# 19.this.getOptions is not a function



报错， this.getOptions is not a function



原因1：less-loader 包版本太高，下载5.0.0



原因2：css-loader style-loader less less-loader@5.0.0这几个包都下载



# 20. Malformed arrow function parameter list



```plain
console.log(typeof res => console.log(res))
```



会报这个错



原因是因为 typeof 会逐个去解析 res 然后 => 然后 console.log



外面加个括号就可以解决







# 21. {  "compilerOptions": {   "baseUrl": "./",   "paths": {     "@/*": ["src/*"]   }  },  "



- setting.json这个文件出错



重启了一下 Path Intellisense这个包



重启了一下 VS CODE



就解决了



# 22. 报错



```plain
request.js?b775:46 Uncaught (in promise) Error: 程序执行遇到异常！异常信息：Cannot read property '_id' of null
    at __webpack_exports__.default (webpack-internal:///./src/utils/request.js:63:27)
```



页面一刷新就报错 => 已刷新就调用getDepartments 哪里用到这个方法就都会报错



解决：



vue热更新的问题 在vscode终端打开就解决了这个问题



# 23. sockjs



bug: sockjs解决



https://www.cnblogs.com/jackzer666/p/13345231.html



https://segmentfault.com/q/1010000005045512
如果切换了本地的网络，也会报错。比如热点关闭了，也会报错，因为开发服务器不知道如何确定访问源



# 24. console.log()打印不出来 打印失败 alert有效果



重启谷歌浏览器默认配置



# 25. prompt获取的是字符串



```javascript
        let num1 = + prompt("请输入")
        let num2 = + prompt("请输入")
        console.log(num1 + num2);//3
```



如果没有前面的+号，打印的是12字符串



# 26. 文件头部 函数注释 官网配置



```plain
https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE#2-%E8%87%AA%E5%8A%A8%E6%B7%BB%E5%8A%A0%E6%96%87%E4%BB%B6%E5%A4%B4%E9%83%A8%E6%B3%A8%E9%87%8A
```



# 27. webpack打包



```plain
webpack打包Cannot use import statement outside a module
```



?



package.json



```plain
  "type": "module",
```



第二个问题：



```plain
The 'mode' option has not been set, webpack will fallback to 'production' for this value.
```



```plain
  "scripts": {
    "build": "webpack --mode development"
  }
```



这样设置能够解决上面的问题，但是main.js里面会很乱



=》为什么？生产模式 代码突然变得很多



=》去掉--mode只是会有警告 但是没关系



# 28. vue脚手架项目



body添加margin: 0 和padding =》如果App.vue文件里面设置了scoped属性 就会出问题



给body添加的属性就不会生效



因为App.vue组件会被注入到public/index.html文件里面去，而设置了scoped，那么样式只会影响scoped，不能够影响public/index.html



# 29. vuex



```plain
Object is not defined
```



出现这个错误的原因是,vuex的版本太高了，和vue的版本不匹配



给vuex降级 讲道 3.1.0左右差不多



# 30. range of null

```javascript
range of null报错时，babel-eslint要降级
```



# 31. props null 

```javascript
 element表单传值问题，如果点击下拉表单1，报错，点击下拉表单2的选项，报错，
 原因可能来自其中的某一个表单，删除其中的表单试试。
 如果是一个表单没有值引起其它的表单报错，这个表单可能一开始就需要初始值。
 如果没有，也不影响，只要程序能够向下进行。
```



# 32. 字符串转为数字

var str = '1';

console.log(typeof +str) // 'number'





# 33. less语法出错？

less语法出错的可能性:

1. import导入 前面没有加@负号 也就是 [@import ]() ‘’ 
2. less语法必须结尾有分号
3. import导入的路径 出错了也会报错





# 40. 权限问题?

```plain
The operation was rejected by your operating system.
```





# 41. 组件名字

```plain
Failed to resolve component: goods-comment-image
If this is a native custom element, make sure to 
exclude it from component resolution via compilerOptions.isCustomElement. 
```

解法：

1. 原本写的

```diff
export default {
  name: 'GoodsComment',
  component: {
    GoodsCommentImage
  },
```

1. 改正后

```diff
export default {
  name: 'GoodsComment',
+  components: {
    GoodsCommentImage
  },
```



# 42. Password field is not contained in a form

问题是input: password输入框必须在form标签里面，如果没有就会弹出这个错误

解决方式，就是要么加一层form，

要么不管它





# 43. Invalid attempt to iterate non-iterable instance.

In order to be iterable, non-array objects must have a [Symbol.iterator]() method.

无效的尝试读写不可读的实例

```javascript
for (const key in obj) 对象要这些去读
for (const key of arr) 数组是 for …… of
```



# 44. typora图片

设置 - 偏好设置 - 无特殊操作 - 图片能够统一存到一个文件夹，这是好事情



# 45. vue emits

```
vue3的emit
```



1. vue3多了一个emit的选项，如果有根元素，无需这个选项
2. 如果没有根元素，需要这个选项。目的是更加规范，因为页面可能写了很多个事件需要更改



如果没有根元素div，但是又没有写emit选项，就会报错



```diff
 Extraneous non-emits event listeners (change) were passed to component but could not 
 be automatically inherited because component renders fragment or text root nodes.
```





# 46.fatal: could not create work tree dir 'gin-vue-admin': Permission denied

```javascript
右键D盘 -> 属性 -> 权限 -> 完全权限 即便报错也没关系 -> 关闭再次打开啊，发现已经√上了
```





# 47. ERROR in Node Sass does not yet support your current environment: Windows 64-bit with Unsupported runtime (93)



看到问题不要慌

去csdn



```plain
我的node版本是 16.0+ 支持的 node-sass最低是6.0+[要去npm搜索node-sass才能发现]
```

版本

```javascript
node-sass: "^6.0.1",
sass-loader: "^10.0.1"
```



# 48. network如果是unavailable 怎么解决

在vue.config.js里面写

```diff
module.exports = {
  devServer: {
    host: '0.0.0.0',
    public: '10.153.224.210:8080', // 该网络地址为你联网的ip地址
    port: 8080,
    https: false,
    hotOnly: false,
    disableHostCheck: true,
  },
}
```



# 49. Uncaught SyntaxError: Cannot use import statement outside a modul



报错原因是：直接在index.html里面引入js，js里面使用了import语法，不能够被浏览器识别，报错



用parcel或者是打包工具启动项目，再进入项目的地址，而不是`手动 ctrl+B`启动的项目，就没关系





# 50. The file will have its original line endings in your working directory
场景：1. 在给一个“之前没有创建git仓库的文件”，创建git仓库，2. git add .的时候遇见了上面的报错
原理就是：对于换行符的处理，出现了问题，先粗略理解。 git config core.autocrlf false是关键，关闭换行符的处理。再次git add .

设置git config core.autocrlf false 如果是false，表示不做换行处理，
如果设置true，表示会把 crlf变成 lf
windows下，会把crlf变成lf
update代码时，会把lf变成crlf

```javascript
git rm -r --cached .

git config core.autocrlf false // 这句是关键

git add .
```