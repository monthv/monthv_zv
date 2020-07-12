## 基础知识

[vbase]()创建基础模板

vue项目运行	

安装依赖[npm install]() 

编译[npm run dev]()

打包[npm run build]()

[import](//import预编译加载
//require执行时加载)	预编译加载

[require](//import预编译加载
//require执行时加载)	执行时加载

一、

#### 1、插值表达式	[{{	}}]()

#### 2、循化	[v-for]()

```vue
<ul>
   <li v-for="item in user">{{item.name}}</li>
</ul>
```

v-for="(item,index) in list"	[item]()循化的每一项	[index]()索引

#### 3、[显示隐藏]()[：]()

```vue
<span v-if="false"> v-if 销毁或创建 DOM </span>
        
<span v-show="true"> v-show 通过css控制显示或隐藏</span>
```

[v-show]()隐藏是[display:'none']()
[v-if]()隐藏是[visibility:hidden]()

[区别：]()

display:none是彻底消失，不在文档流中占位，浏览器也不会解析该元素

visibility:hidden是视觉上消失了，可以理解为透明度为0的效果，在文档流中占位，浏览器会解析该元素；

[v-show]()

v-show仅仅控制元素的显示方式，通过display属性的none

当我们需要[经常]()切换某个元素的显示/隐藏时，使用v-show会更加节省[性能]()上的开销

[v-if]()

操作DOM元素 性能低

v-if会控制这个[DOM节点]()的存在与否。

如果在运行时[条件很少改变]()，则使用 v-if 较好。

#### 4、双向绑定	[v-model]()

```vue
<input v-model="input" type="text"/><span>{{input}}</span>
```

#### 5、单项绑定	[v-bind]()

#### 6、事件绑定	[v-on]()

[v-on]():事件名称

```vue
<button v-on:click="newClick()">按钮</button>
```

#### 7、vue[属性]()

挂载vue对象到指定的Dom元素上	[el]()

挂载	[element]()

数据源	[data]()

方法	[methods]()

```vue
<div id="app">
    
</div>
var vm=new Vue({
    el:'#app'
    data:{    
    },
    methods:{    
    },
    )};
```

#### 8、组件	[component]()	代码复用

组件化/模块化

#### 9、[MVVM]() 

model view viewmodel