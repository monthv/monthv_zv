# 路由

#### 嵌套路由

嵌套路由和嵌套组件之间的匹配是个很常见的需求，使用 vue-router 可以很简单的完成这点。

```vue
<div id="app">
  <router-view></router-view>
</div>
```

`<router-view>` 是一个顶级的外链。它会渲染一个和顶级路由匹配的组件

官方文档：https://github.com/vuejs/vue-router/blob/1.0/docs/zh-cn/nested.md

#### 路由默认主页

在[routes.js](https://github.com/vuejs/vue-router/blob/1.0/docs/zh-cn/nested.md)文件中加{[path](https://github.com/vuejs/vue-router/blob/1.0/docs/zh-cn/nested.md):'/',[redirect](https://github.com/vuejs/vue-router/blob/1.0/docs/zh-cn/nested.md):'/填地址'}

在routes.js文件中加 [mode:'history']()去掉#号

const createRouter = () => new Router({

  routes,

 [mode:'history']()

})

1、用于如果找不到界面就返回默认首页

[historyApiFallback]():{

index:'/index.html',

}

[匹配规则]() 	在任何情况下都使用自己设置的主页

```vue
historyApiFallback: {
			rewrites: [{
				from: /.*/g,
				to: '/page/index.html'
			}]
		},
```

[细节]()：to里面的参数是不能加点