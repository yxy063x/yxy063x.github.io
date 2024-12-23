# 搭建项目

## vue-cli

- 全局安装 vue 命令行工具

  ```shell
  sudo npm install -g @vue/cli
  
  vue -V
  ```
  
- 创建本地项目

  ```shell
  # 进入创建项目的目标父级目录
  vue create goldmine-admin
  ```
  
  预设选择
  
  - Please pick a preset: Manually select features
  - Check the features needed for your project: Babel, PWA, Router, Vuex, CSS Pre-processors, Linter, Unit, E2E
  - Choose a version of Vue.js that you want to start the project with 2.x
  - Use history mode for router? (Requires proper server setup for index fallback in production) Yes
  - Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Sass/SCSS (with dart-sass)
  - Pick a linter / formatter config: Prettier
  - Pick additional lint features: Lint on save
  - Pick a unit testing solution: Jest
  - Pick an E2E testing solution: Cypress
  - Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
  - Save this as a preset for future projects? Yes
  - Save preset as: test
  
- 运行项目

  ```shell
  cd goldmine-admin
  npm run serve
  ```
  
- 修改 git 分支

  ```shell
  git branch -m master main
  ```
  
- GitHub 创建项目并同步

  - 创建repository：goldmine-admin
  
  - 同步本地项目
  
    ```shell
    cd goldmine-admin
    git remote add origin git@github.com:yxy063x/goldmine-admin.git
    git push -u origin main -f
    
    git checkout -b develop main
    git push -u origin develop
    ```
    
    
  

# 导入和导出

## import

- 在一个文件或模块中可以有多个

- 全部导入

  ```javascript
  import * as _A from "./A.js" 
  ```

- import在引入文件路径时，引入一个依赖包，不需要相对路径。

  ```javascript
  import app from ‘app’;
  ```

  但引入一个自己写的 js 文件，需要相对路径。

  ```javascript
  import app from ‘./app.js’;
  ```

  引入第三方插件，不需要相对路径。

  ```javascript
  import Vue from 'vue';
  ```

- 导入css文件。

  ```javascript
  import 'vue-video-player/src/custom-theme.css';
  ```

  如果是在.vue文件中，需要在其外面套一个style

  ```vue
  <style>
    @import './test.css';
  </style>
  ```

- import '@…'的语句，@等价于 /src 这个目录，避免写麻烦而又易错的相对路径

  ```javascript
  import { getCodeImg } from "@/api/login";
  ```

- Vue使用import ... from ...来导入组件，库，变量等。而from后的来源可以是js，vue，json。在 webpack.base.conf.js 中设置；

  这3类可导入文件，js和vue是可以省略后缀，json不可以省略后缀；

  如果js和vue同名且在同一个文件夹下，js 优先级高于vue；

  ```javascript
  module.exports = {
        resolve: {
          extensions: ['.js', '.vue', '.json'],
          alias: {
            '@': resolve('src')
          }
        }
      ...
      }
  ```

  from后的来源除了文件，还可以是文件夹，那么在文件夹中的package.json存在且package.main设置正确的情况下，会默认加载package.json的package.main指定的js；若不满足，则加载index.js；若不满足，则加载index.vue。

  ```javascript
  import test from './components'
  ```

- 导入外部的模块，并立即执行

  ```javascript
  import './test'
  ```

  

## export

- 在一个文件或模块中可以有多个



## export default

- 在一个文件或模块中仅有一个
- 通过export方式导出，在导入import时要加花括号{ }，export default 则不需要 { }



# 组件

在 vue 中，组件是可以重复使用的 vue 实例，拥有一个名为 options 的对象，用于定义组件的属性、方法、生命周期等。而父子组件，是一种层级关系，其中一个组件（父组件）内部使用了另一个组件（子组件）。

- 父组件向子组件传递属性，子组件声明 props
- 子组件通过$emit 方法触发自定义事件，父组件通过@childEvent （$on）监听子组件触发的自定义事件，并在事件处理函数中接收子组件传递的数据

```vue
Vue.component(component)
```



# 插件

- 如果插件是一个对象，必须提供 install 方法。
- 如果插件是一个函数，它会被作为 install 方法。install 方法调用时，会将 Vue 作为参数传入。
- 该方法需要在调用 new Vue() 之前被调用。

```vue
Vue.use(plugin)
```

