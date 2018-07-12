# vuex状态管理

## 安装
```bash
    npm install vuex --save
```

## 引入目录如下

```js
    --> main.js
    --> store 文件夹
        --> actions.js
        --> getters.js
        --> index.js
        --> mutation-types.js
        --> mutations.js
        --> state.js
```


## state.js

```js
    // state是用来存放静态数据的地方

    export const state = {
      singer:'我是原始数据'
    }
```

## getters.js

```js
    // state中的存放的数据要通过getters来获取

    export const getters = {
      getSinger (state) {
        return state.singer
      }
    }
```

## mutations.js --- mutation-types.js

```js

    //mutations用于改变state存放的数据

    --> mutations.js

    import * as types from './mutation-types';

    export const mutations = {
      [types.SET_SINGER](state,val){
        state.singer = val
      }

    }

    --> mutation-types.js

    export const SET_SINGER = 'SET_SINGER';

```

## actions.js

```js
    // actions是用于较为复杂的改变state中存放的数据

    import * as types from './mutation-types'

    export const actions = {
      changeSinger:({ commit },val) => commit('SET_SINGER',val),

      // 这里就是复杂的改变的demo

      // changeSinger:({ commit },val) => {
      //   let save = val;
      //   commit('changeSinger',[])
      //   setTimeout(()=>{
      //     if(success){
      //
      //     }else{
      //       commit('changeSinger',save)
      //     }
      //
      //   },3000)
      //
      // },

    }
```

## index.js

```js

    import Vue from 'vue';
    import Vuex from 'vuex';

    import { actions } from './actions.js';
    import { mutations } from './mutations.js';
    import { getters } from './getters.js';
    import { state } from './state.js';

    // vuex 自带的logger
    import createLogger from 'vuex/dist/logger';

    const logger = createLogger({
      collapsed: false, // 自动展开记录的 mutation
      filter (mutation, stateBefore, stateAfter) {
        // 若 mutation 需要被记录，就让它返回 true 即可
        // 顺便，`mutation` 是个 { type, payload } 对象
        return mutation.type !== "aBlacklistedMutation"
      },
      transformer (state) {
        // 在开始记录之前转换状态
        // 例如，只返回指定的子树
        return state.subTree
      },
      mutationTransformer (mutation) {
        // mutation 按照 { type, payload } 格式记录
        // 我们可以按任意方式格式化
        return mutation.type
      },
      logger: console, // 自定义 console 实现，默认为 `console`
    })

    Vue.use(Vuex);
    // 这是判断是否是生产环境的  如果是生产环境就不打印logger
    const debug = process.env_NODE_DEV !== 'production'

    export default new Vuex.Store({
      actions,
      getters,
      state,
      mutations,
      plugins: debug ? [createLogger()] : []
    })

```

## main.js

```js
    // 在main.js中引入
    import store from './store/index'

    new Vue({
      el: '#app',
      render: x=>x(App),
      /* function(x){
         return x(App)
       },*/
      store
    })
```