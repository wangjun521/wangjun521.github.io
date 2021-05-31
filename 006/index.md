# taro3.x版本使用vue2.x版本注意事项


 照例官方文档安装脚手架并且初始化项目

- app.js中App的初始化已去除`new Vue`来创建实例, 可直接使用对象来初始化
- 项目中`vuex`可照常使用
- 可在项目的 `config`文件夹下的`dev``prod`文件内设置`defineConstants`字段来使用不同环境下的变量 但要注意 json字段的`[key]`值必须是`number` 或者`JSON.stringify(xx)`类型
- 项目中如果使用css预编译器 不能在app的样式文件中定义`mixin` 可单独创建预编译文件通过`config`下的`index`文件中样式属性设置来引入 这样可在全局调用到
