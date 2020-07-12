# 基础架构

## Storage封装

#### Cookie、localStorage、sessionStorage三者区别

- 存储大小：Cookie4K、Storage5M
- 有效期：Cookie拥有有效期、Storage永久存储
- Cookie会发送到服务器端，存储在内存中，Storage只存储在浏览器端
- 路径：Cookie有路径限制，Storage只存储在域名下
- API：Cookie没有特定的API，Storage有对应的API

#### 为什么要封装Storage

- Storage本身有API，但是只是简单的key/value形式

- Storage只存储字符串，需要人工转换成json对象

- Storage只能一次性清空，不能单个清空

  [配置文件]()

```js
// Storage封装
const STORAGE_KEY='mall';
export default{
    //存储值
    setItem(key,value,module_name){
        if(module_name){
            let val=this.getItem(module_name);
            val[key]=value;
            this.setItem(module_name,val);
        }else{
            let val=this.getStorage();
            val[key]=value;
            window.sessionStorage.setItem(STORAGE_KEY,JSON.stringify(val));
        }  
    },
    //获取值
    //module_name  获取某个模块的下面的属性   比如user下面的userName
    getItem(key,module_name){
        if(module_name){
            let val=this.getItem(module_name);
            if(val) return val[key];
        }
        return this.getStorage()[key];
    },
    //获取所有数据
    getStorage(){
        return JSON.parse(window.sessionStorage.getItem(STORAGE_KEY) || '{}');
    },
    //清空某个值
    clear(key,a,module_name){
        let val=this.getStorage();
        if(module_name){
            delete val[module_name][key][a];
        }else{
            delete val[key];
        }
        window.sessionStorage.setItem(STORAGE_KEY,JSON.stringify(val));
    }
}
```

```vue
<script>
import storage from './storage'
export default {
  data(){
    return{
    }
  },
  mounted(){
    storage.setItem('Name',1);//存储某个值
    storage.setItem("Name",{Man:1},"user");//存储值在user下面
    storage.clear('Name');//清空某个值
    storage.clear('Name','user');//清空user下面的某个值
  }
}
</script>
```

## 接口

#### 接口错误拦截

安装axios	[npm install axios]()

[同时发送多个请求]()

```js
axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // Both requests are now complete
  }));
```

```js
import Vue from "vue";
import axios from 'axios';
import VueAxios from 'vue-axios';//把作用域对像挂载到vue实例上面。可以使用this调用
import App from "./App.vue";
import router from "./router";

//设置基础值
//根据前端的跨域方式做调整 /a/b : /api/a/b=>/a/b
axios.defaults.baseURL='/api';//接口代理模式
axios.defaults.timeout=8000;//超时时间

//接口错误拦截
axios.interceptors.response.use(function(response){
  let res=response.data;//获取接口返回的值
  //status 状态码
  //状态码是0代表成功
  if(res.status == 0){
    return res.data;
  }else if(res.status == 10){//状态码10代表未登录
    window.location.href='/#/login';
  }else{
    //错误信息
    alert(res.msg)
  }
});

Vue.use(VueAxios,axios);//挂载
Vue.config.productionTip = false;//生产环境提示
```

#### 接口环境设置

[package.json]()

```json
"scripts": {
    "serve": "vue-cli-service serve --mode=development",//开发
    "test": "vue-cli-service serve --mode=test",//测试
    "build": "vue-cli-service build --mode=production",//线上
  },
```

[env.js]()

```js
//接口环境设置
let baseURL;
//process进程
//process.env.NODE_ENV 获取当前node.js进程的环境变量
//process.env.NODE_ENV 获取当前传过来的参数
switch (process.env.NODE_ENV) {
  case "development":
    baseURL = "http://dev-mall-pre.springboot.cn/api";
    break;
  case "test":
    baseURL = "http://test-mall-pre.springboot.cn/api";
    break;
  case "pro":
    baseURL = "http://mall-pre.springboot.cn/api";
    break;
  default:
    baseURL = "http://mall-pre.springboot.cn/api";
    break;
}

export default {
  baseURL
};

```

[main.js]()

```js
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios"; //把作用域对像挂载到vue实例上面。可以使用this调用
import App from "./App.vue";
import env from "./env";

//设置基础值
//根据前端的跨域方式做调整 /a/b : /api/a/b=>/a/b
axios.defaults.baseURL = "/api"; //接口代理模式
axios.defaults.timeout = 8000; //超时时间
axios.defaults.baseURL = env.baseURL; //根据环境变量获取不同的请求地址
```

如果要自定义环境的话添加自定义文件如：[.env.te_st]()	te_st是环境名

里面代码：NODE_ENV='te_st'

## Mjock设置

#### Mock：模拟数据

#### 作用

- 开发阶段，为了高效率，需要提前Mock
- 减少代码冗余、灵活插拔
- 减少沟通。减少接口联调时间

#### Mock方式

- 本地创建json
- easy-mock平台
- 集成Mock API

[本地创建json]()

[login.json]()文件

```js
{
	"status":0,
    "data":{
        "id":12,
        "username“：”admin",
        "email":"admin@qq.com",
        "phone":null,
        "role":0,
        "createTime"1479048325000,
        "updataTime":1479048325000
    }
}
```

[App.vue]()文件

```vue
<script>
export default {
  data() {
    return {
        res:{}
    };
  },
  mounted() {
  		this.axios.get('/login.json').then((res)=>{
            this.res=res;
        });
  }
};
</script>
```

