# mobx
[问题] mobx-react observer 对传入的props做了浅比较，所以传递相同的值会有问题  

[问题] 怎么才能不把生产环境的 mock 文件打包进来  
[原因及方案] 我是这么做的
  - 首先添加了一个 npm script: `"start:no-mock": "cross-env REACT_APP_MOCK=none npm start"`
  - 其次在 index.js 文件里面：
  ```js
  if (process.env.NODE_ENV === 'development' && process.env.REACT_APP_MOCK !== 'none') {
    import('../mock')
  }
  ```

[问题] HMR 导致修改之后 mobx 的数据都变成初始数据了  
[原因及方案] react-hot-loader 遇到更新的时候会 rerender 组件，之前的 hot 挂载在 App 上，App 里面用了 provider 去传递数据，每次 rerender 都会重新传数据，所以数据就变成初始的了，hot 方法包裹的组件应该不包括它