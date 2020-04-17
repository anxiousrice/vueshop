# vue_shop

> a vue.js project by lideren

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run all tests
npm test
```

1，技术栈

前端 vue vue-router element-UI Axios Echarts  后端 node.js express mysql jwt sequelize

2,项目初始化

vue -cli  router 配置element-ui axios库 初始化git仓库

3.后台项目环境配置

php-study安装 sql还原 测试api接口



登陆页面逻辑

登陆输入密码和用户名 调用后台接口认证 之后跳转 存在跨域问题使用token维持状态

##按需导入element-ui组件并注册

```
import Vue from 'vue'
import { Button, Form, FormItem, Input, Message } from 'element-ui'

Vue.use(Button)
Vue.use(Form)
Vue.use(FormItem)
Vue.use(Input)
```

##登陆界面template

```
<template>
  <div class="login_container">
    <div class="login_box">
      <!-- 头像区域 -->
      <div class="avatar_box">
        <img src="../assets/logo.png" alt="">
      </div>
      <!-- 登录表单区域 -->
      <el-form ref="loginFormRef" :model="loginForm" :rules="loginFormRules" label-width="0px" class="login_form">
        <!-- 用户名 -->
        <el-form-item prop="username">
          <el-input v-model="loginForm.username" prefix-icon="iconfont icon-user"></el-input>
        </el-form-item>
        <!-- 密码 -->
        <el-form-item prop="password">
          <el-input v-model="loginForm.password" prefix-icon="iconfont icon-3702mima" type="password"></el-input>
        </el-form-item>
        <!-- 按钮区域 -->
        <el-form-item class="btns">
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info" @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

```

iconfont添加一些图标库，导入图标加类

表单属性绑定 添加model属性，密码框type设定为passworld，添加预验证，根据返回data的状态码判断结果

将登录成功之后的 token，保存到客户端的 sessionStorage 中

​    //  1.1 项目中出了登录之外的其他API接口，必须在登录之后才能访问

​    //  1.2 token 只应在当前网站打开期间生效，所以将 token 保存在 sessionStorage 中

添加路由导航守卫，添加退出功能 销毁token

