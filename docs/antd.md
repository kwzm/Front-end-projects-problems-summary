# antd
[问题] treeselect组件，指定 disableCheckbox 会有 bug   
[原因及方案] 详情见[https://github.com/ant-design/ant-design/issues/10360](https://github.com/ant-design/ant-design/issues/10360)，方法就是给需要禁用复选框的元素添加 class，然后用 css 来实现禁用效果