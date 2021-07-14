### 引入vue-router

1. 通常是在`App.vue`文件中导入路由对象，并且调用`Vue.use(VueRouter)`；
2. 创建路由实例，并且传入路由映射配置；
3. 在Vue实例中挂载创建的路由实例

### 使用vue-router的步骤

1. 创建路由组件；
2. 配置路由映射：组件和路径的对应关系；
3. 使用路由：通过`<router-link>`和`<router-view>`

**例：**

* 首先定义两个组件`Home.vue`和`About.vue`

* 接着新建`router.js`，并引入上面两个组件：

  ```js
  import Home from '../components/Home'
  import About from '../components/About'
  ```

  定义路由规则并新建路由：

  ```js
  const routes = [
    {
      path: "/",
      redirect: "/home"
    },
    {
      path: "/home",
      component: Home
    },
    {
      path: "/about",
      component: About
    }
  ]
  
  var router = new VueRouter({routes})
  ```

  注：路由规则routes是数组，但注册路由对象的时候使用的是对象

* 在需要使用路由的地方（例如`App.vue`）使用`<vouter-link>`和`<vouter-view>`

  ```vue
  <router-link to="/home">Home</router-link>
  <router-link to="/about">About</router-link>
  <router-view></router-view>
  ```

* 在项目入口文件中引入并注册vue-router

  ```js
  import VueRouter from 'vue-router'
  Vue.use(VueRouter)
  new Vue({
      router,
      render: h => h(App),
  }).$mount('#app')
  ```

**`$router`和`$route`的区别：**

* `$router`指的是整个路由实例，这是一个全局的对象，包含了所有的路由和对应的属性
* `$route`指的是跳转的路由对象，每个路由都会有一个route对象，是一个局部的对象

### 动态路由

 在路由规则中定义：

```js
const routes = [{
    path: "/user/:userId".
    component: User
}]
```

其中`:userId`为动态可变的部分，根据`<router-link>`中的具体使用而改变：

```vue
<router-link to="/user/aaa">AAA</router-link>
<router-link to="/user/bbb">BBB</router-link>
```

### 嵌套路由

在路由规则中定义：

```js
const routes = [{
    path: "/home",
    component: Home,
    children: [{
        path: "profile",
        component: Profile
    },{
        path: "posts",
        component: Posts
    }]
}]
```

接着在`Home.vue`组件中引入`Profile.vue`和`Posts.vue`组件，同时使用`<router-link>`:

```vue
<vouter-link to="/home/profile">Profile</vouter-link>
<vouter-link to="/home/posts">Posts</vouter-link>
```

### 传递数据

* 通过动态路由传递：

  在路由规则中定义：

  ```js
  const routes = [{
      path: "/user/:userId".
      component: User
  }]
  ```

  即可在`User.vue`组件中使用`$route.params.userId`获取

* 通过query传递：

  在使用`<router-link>`的时候`to`可以传递一个对象，如

  ```js
  {
      path: "user",
      query: {
          name: "yap",
          age: 18
      }
  }
  ```

  即可在`User.vue`组件中使用`$route.query.name`获取

### 导航守卫

* 全局前置守卫：

  可以使用`router.beforeEach()`注册一个全局前置守卫：

  ```js
  router.beforeEach((to, from, next) => {
      // to指目的指向的route
      // from指正要离开的route
      // next是一个函数，指路由的跳转行为
  })
  ```

* 路由独享的守卫：

  可以直接在路由配置上定义







