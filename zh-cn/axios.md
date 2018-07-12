# axios与封装

## 安装

```bash
    npm install axios --save
```
## 引用目录如下

```js
    --> static 文件夹 --> projectConifg 文件夹 --> projectCongin.js

    --> https 文件夹

        --> filter.js
        --> https.js
        --> url.js
```

## filter.js

> filter.js  添加请求拦截器 以及一些配置

```js

    import axios from "axios";

    // axios可以创建一个实例
    export const Axios = axios.create({
      timeout: 10000,
      responseType: "json",
      withCredentials: true, // 是否允许带cookie这些
      headers: {
        "Content-Type": "application/x-www-form-urlencoded;charset=utf-8"
      }
    });

    //POST传参序列化(添加请求拦截器)
    Axios.interceptors.request.use(
      config => {
        return config;
      },
      error => {
        return Promise.reject(error.data.error.message);
      }
    );

    //返回状态判断(添加响应拦截器)
    Axios.interceptors.response.use(
      res => {
        return res;
      },
      error => {
        return Promise.reject(error);
      }
    );


    /**
     * 封装get方法
     * @param url
     * @param data
     * @returns {Promise}
     */
    export function GET(url,params={}){
      return new Promise((resolve,reject) => {
        Axios.get(url,{
          params:params
        })
          .then(response => {
            resolve(response.data);
          })
          .catch(err => {
            reject(err)
          })
      })
    }


    /**
     * 封装post请求
     * @param url
     * @param data
     * @returns {Promise}
     */

    export function POST(url,data = {}){
      return new Promise((resolve,reject) => {
        Axios.post(url,data)
          .then(response => {
            resolve(response.data);
          },err => {
            reject(err)
          })
      })
    }


    /**
     * 封装put请求
     * @param url
     * @param data
     * @returns {Promise}
     */

    export function PUT(url,data = {}){
      return new Promise((resolve,reject) => {
        Axios.put(url,data)
          .then(response => {
            resolve(response.data);
          },err => {
            reject(err)
          })
      })
    }

    /**
     * 封装delete请求
     * @param url
     * @param data
     * @returns {Promise}
     */

    export function DEL(url,data = {}){
      return new Promise((resolve,reject) => {
        Axios.delete(url,data)
          .then(response => {
            resolve(response.data);
          },err => {
            reject(err)
          })
      })
    }



```

## https.js 请求操作

> 在https.js中专门进行请求操作

```js

    import {Axios} from './filter'  // 拦截操作
    import {url} from './url'       // 请求地址

    export const https = {}

    https.getIndexInfo = (params) => {
      return new Promise((resolve, reject) => {
        Axios.get(url.getIndexInfo, params).then(res => {
          resolve(res);
        }).catch(err => {
          reject('getIndexInfo',err);
        })
      })
    }

    _http = https;  // 请求操作存放在全局中

```

## url.js 请求地址

> url.js中专门存放请求地址

```js

    export const url = {};
    //配置项数据
    url.getIndexInfo = '/nodeServer/';   // 首页

```

## 配置全局

> 以script的方式引入index.html

> static 文件夹 --> projectConifg 文件夹 --> projectCongin.js

```js
    var projectConfig = { // 多个地方用得到的地方放这里

    }

    var _http = null;  // 只有一个用得到的地方就单独一个
```

