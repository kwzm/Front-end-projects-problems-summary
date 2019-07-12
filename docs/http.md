# http
[问题] ajax 无法截获 302 状态码

[问题] 本地开发时的 cookie 校验问题  
[原因及方案] 因为登录是用的服务器上现成的登录页面，权限校验是通过 cookie 来实现的所以我需要设法让我的本地域名下也能保存到后台返回的 cookie，这样本地开发时才能校验成功，所以我通过 http-proxy-middle 设置了 /login 页面的代理，代理到测试服务器上的登录页面，这样登录成功后我本地域名下也有了 cookie。
    ```js
        const proxy = require('http-proxy-middleware')
    
        module.exports = function(app) {
          // 代理api请求
          app.use(
            proxy('/api', {
              target: process.env.REACT_APP_DEV_SERVER,
              pathRewrite: { '^/api': '' },
              changeOrigin: true,
            })
          )
          // 代理登录、退出页面
          app.use(
            proxy([process.env.REACT_APP_LOGIN_URL, '/public', '/auth/check', '/logout'], {
              target: process.env.REACT_APP_DEV_SERVER,
            })
          )
        }
    ```