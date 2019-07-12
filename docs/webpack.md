# webpack
[问题] 每次修改一个 chunk 如果和第三方库有关的代码，则会导致很多 chunk 打包的 hash 变化  
[原因及方案] 这个是正常的，因为 webpack 的 splickChunk 结合 import() 的原因导致的

[优化] hard-source-webpack-plugin 可以提高再次编译速度