# ng-antd-theme-generator
此插件是在[antd动态换肤](https://github.com/mzohaibqc/antd-theme-generator)的基础上修改，对ng-zorro-antd的动态换肤的实现； 
This script generates color specific styles/less file which you can use to change theme dynamically in browser

## 环境要求
- angular 7.x
- ng-zorro-antd 7.x

## 实例:

```
const { generateTheme } = require('antd-theme-generator');

const options = {
  antDir: path.join(__dirname, "./node_modules/ng-zorro-antd"), //ng-zorro-antd包位置
  stylesDir: path.join(__dirname, "./src/theme"),               //指定皮肤文件夹
  varFile: path.join(__dirname, "./src/theme/variables.less"),  //自己设置默认的主题色,动态定义less变量值
  mainLessFile: path.join(__dirname, "./src/theme/index.less"),
  indexFileName: "./src/index.html",
  outputFilePath: path.join(__dirname, './src/assets/color.less'), //输出到什么地方
  themeVariables: [
    // 这里写要改变的主题变量
    '@primary-color',
    '@success-color',
    '@warning-color',
    '@error-color',
    '@info-color',
    '@layout-header-background'
  ],
  generateOnce: false
}

generateTheme(options).then(less => {
  console.log('Theme generated successfully');
})
.catch(error => {
  console.log('Error', error);
})
```
## Note: include all color variables in `varFile` that you want to change dynamically and assign them unique color codes. Don't assign same color to two or more variables and don't use `#fff`, `#ffffff`, `#000` or `#000000`. If you still want white or black color as default, slightly change it e.g. `#fffffe` or `#000001` which will not replace common background colors from other components.

Add following lines in your main html file

```
<body>
    <link rel="stylesheet/less" type="text/css" href="assets/color.less">
    <app-root>
    </app-root>
    <script src="assets/less.min.js"></script>
</body
```

Now you can update colors by updating less variables like this

```
window.less.modifyVars({
  '@primary-color': '#0035ff'
})
```
