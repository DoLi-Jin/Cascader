1、背景
    elementUI中目前只提供了单选的级联选择器，
    但是项目变化多端，
    所以在某次，项目要求 多选级联选择器 的时候，
    就"拼凑"了一个这样的小功能
    
2、重点
    使用了   elementUI中的select选择器（https://element.eleme.io/#/zh-CN/component/select）
    加       elementUI中的tree树形控件（https://element.eleme.io/#/zh-CN/component/tree）
    组合成了一个类似多选级联选择器的功能。
    
3、警告
    项目中的两行 css样式 很重要。请注意
    （此处有坑）css样式会覆盖其他下拉框，并且使用/deep/不起作用，所以要使用行内样式或者独立的全局样式
    
# cascader

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
