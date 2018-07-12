# router路由

```js
    import Vue from 'vue'
    import Router from 'vue-router'

    // 引入的组件   我这里使用了路由懒加载所以不用import导入的形式了
    // import home from '@/components/home.vue'

    //路由懒加载   有三种写法 这个是最好的写法 最直观明确的写法
    const home = r => require.ensure([], () => r(require('@/components/home.vue')), 'home');

    Vue.use(Router);

    const routes = [
      {
        path: '/',
        name: 'home',
        component: home
      }
    ]

    const VueRouter = new Router({
      // model:'history',
      // base:__dirname,
      routes
    })

    export default VueRouter


    /*
      路由拦截
      1、在routes中添加   meta:{requireAuth:true}  配置此条，进入页面前判断是否需要登录
      2、路由拦截方法在main.js中
      router.beforeEach((to, from, next) => {
     if (to.matched.some(res => res.meta.requireAuth)) { // 验证是否需要登陆
      if (sessionStorage.getItem('sid')) { // 查询本地存储信息是否已经登陆
       next();
      } else {
       next({
        path: '/login', // 未登录则跳转至login页面
        query: {redirect: to.fullPath} // 登陆成功后回到当前页面，这里传值给login页面，to.fullPath为当前点击的页面
        });
      }
     } else {
      next();
     }
    });
      3、登录成功后
      sessionStorage.setItem('sid', res.data.data.sid); // 设置本地存储信息
      this.$router.push(this.$route.query.redirect); // 跳转至前一页，this.$route.query.redirect是获取上面传递过来的值
     */

```