# vue-typescript-template-ui

一个非常简单的为[Vue2.0][1]和[TypeScript2.0][2]准备的项目开发环境，可以帮助你快速地开始一个项目的开发。

# 特性

- 引入了Vue 2.0全家桶的环境
- 配置好了webpack
- 配置好了一个UI库 - [element-ui][3]，让你开箱即用
- 使用了 TypeScript2.0 以后的新特性`@types`
- 由于Vue2.0采用ES6编写，类型声明中含有Typescript不支持的ES6特性，增加了 TypeScript2.0 对 [Promise][4] 等`es6`特性的支持
- 引入lodash，快速开启FP

有个这些特性，无需在开发环境的搭建上煞费苦心，你可以轻松地将本项目作为你的脚手架代码进行项目开发。

# 快速上手

安装依赖
```
npm install
```
开发测试：
```
npm run dev
```
部署到生产环境：
```
npm run build
```

# 主题

关于主题的配置可以参考 [custom-theme][5]

基本的配置过程如下：

- **安装element-theme**：
```
npm i element-theme -D
```

- **安装element-theme-default**
```
npm i element-theme-default -D 
```

- **生成变量文件**

```
node_modules/.bin/et -i
```
![image_1b92frkkv1g7h7fo1pd41kp31k55m.png-13.9kB][6]

运行成功后，在你的项目根目录下会生成一个基于CSS4.0编写的`element-variables.css`，打开文件，可以编写你的主题配色：

![image_1b92fv4b81jr56i5o5l4o0h4r1g.png-75.2kB][7]


- **生成主题文件**
在上一步编辑好 `element-variables.css` 后，执行此步骤:
```
node_modules/.bin/et
```

![image_1b92fs857n5d9k2car8did0g13.png-15.2kB][8]

这里你也可以加上`-w`参数进行实时编译。

- **在项目中引入**

注意，只需要引入`index.css`
```
import './theme/index.css';
```

接下来，你就可以使用自己的主题了。

# 库

name | version
--- | ---
typescript | 2.0.0+
Vue | 2.0.0+
Vue Router | 2.0.0+
vue-resource | 0.9.3
lodash | 4.0.0+
element-ui | 1.0.0+


# 使用Typescript开发Vue要注意的点

## Typescript2以前

声明文件（.d.ts文件）是在TypeScript中使用现有JavaScript库的一个基本组成部分。

所有的js库在引入ts时，都必须顺带地加入类型声明文件（d.ts）,早期，有一个非常出色的库——[DefinitelyTyped][9]，它拥有一些主流的js库的类型声明文件。此外，为了更便捷地进行安装，还有一个非常强大的ts类型声明管理库——[typings][10]，它允许你通过这样的方式进行安装一个库的类型声明文件：

首先全局安装typings：
```
npm install typings -g
```
推荐采用这种方式进行一个类型定义库的安装：
```
typings install dt~vue --global --save
```
然后，项目根目录下会出现typings目录，结构如下：
![image_1b92hf66j18vo1ic71tcbcp1iac1t.png-8.5kB][11]

index.d.ts 的内容如下：参见ts的[三斜线指令][12]和[模块解析][13]
```
/// <reference path="globals/vue/index.d.ts" />
```

如此一来，我们可以在当前项目目录的任意位置采用如下方式导入Vue:

```
import * as Vue from 'vue';
```

但凡是会引入ts的库，如vue全家桶，或者lodash，都必须通过上述方式获取dts类型声明文件。

但是，Typescript2开始有了一些变化，请看下文。

## Typescript2以后

参见微软的这篇博文：[The Future of Declaration Files][14]

总的意思就是，**在TypeScript 2.0中获取类型声明除了npm之外不需要任何工具。**

比如，想要引入lodash，只需要执行:
```
npm install --save @types/lodash
```
然后你就可以直接使用了：
```
import * as _ from "lodash";
_.padStart("Hello TypeScript!", 20, " ");
```

此外，目前在使用Typescript2 + Vue2遇到的问题，及其解决办法整理如下：

issue | solution
--- | ---
typescript编译表示不认识vue声明文件中的类型Promise | 安装es6-prommise `npm i @types/es6-promise -save`
指令递归会报错，提示堆栈溢出 | 尚未解决



  [1]: https://github.com/vuejs/vue
  [2]: https://github.com/Microsoft/TypeScript
  [3]: https://github.com/ElemeFE/element
  [4]: https://github.com/stefanpenner/es6-promise
  [5]: http://element.eleme.io/#/en-US/component/custom-theme
  [6]: http://static.zybuluo.com/a472590061/jg8g8a6392ppmohabnoh7qii/image_1b92frkkv1g7h7fo1pd41kp31k55m.png
  [7]: http://static.zybuluo.com/a472590061/6oweqbrqjvfm221l3b64ny81/image_1b92fv4b81jr56i5o5l4o0h4r1g.png
  [8]: http://static.zybuluo.com/a472590061/64vc46bkcp3yaayxf6oimqtw/image_1b92fs857n5d9k2car8did0g13.png
  [9]: https://github.com/DefinitelyTyped/DefinitelyTyped
  [10]: https://github.com/typings/typings
  [11]: http://static.zybuluo.com/a472590061/crvbo8k38quhhywmn1j8pcz9/image_1b92hf66j18vo1ic71tcbcp1iac1t.png
  [12]: https://www.tslang.cn/docs/handbook/triple-slash-directives.html
  [13]: https://www.tslang.cn/docs/handbook/module-resolution.html
  [14]: https://blogs.msdn.microsoft.com/typescript/2016/06/15/the-future-of-declaration-files/