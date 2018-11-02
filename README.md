# 基础

## 动机

**styled-components是我们对于如何增强 React 组件中 CSS 表现这个问题的思考结果**
通过聚焦于单个用例,我们设法优化了开发者的体验和面向终端用户的输出.

除了提升开发者体验外, styled-components 同时提供:

- **Automatic critical CSS:** styled-components keeps track of which components are rendered on a page and injects their styles and nothing else, fully automatically. Combined with code splitting, this means your users load the least amount of code necessary.
- **解决了 class name 冲突:** styled-components 为样式生成唯一的 class name. 开发者不必再担心 class name 重复,覆盖和拼写错误的问题.
- **Easier deletion of CSS:** it can be hard to know whether a class name is used somewhere in your codebase. styled-components makes it obvious, as every bit of styling is tied to a specific component. If the component is unused (which tooling can detect) and gets deleted, all its styles get deleted with it.
- **Simple dynamic styling:** adapting the styling of a component based on its props or a global theme is simple and intuitive without having to manually manage dozens of classes.
- **Painless maintenance:** you never have to hunt across different files to find the styling affecting your component, so maintenance is a piece of cake no matter how big your codebase is.
- **Automatic vendor prefixing:** write your CSS to the current standard and let styled-components handle the rest.

通过 styled-components 绑定样式到组件,开发者可以在编写熟知的 CSS 同时也获得上述全部的益处.
## 安装
从 npm 安装 styled-components :
```
npm install --save styled-components
```
>注意
>
>想试用新的 styled-components v4 beta? 现在可以通过如下方式安装:
>```
>npm install --save styled-components@beta
>```

强烈推荐使用 styled-components babel 插件(当然这不是必须的).它提供了许多益处,比如更清晰的类名,SSR 兼容性,更小的包等等.

```
npm install --save-dev babel-plugin-styled-components
```

然后确保插件 babel-plugin-styled-components 添加到`.babelrc`中:
```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"],
  "plugins": ["babel-plugin-styled-components"]
}
```

> 注意
>
>如果你的项目中还没有安装 babel,请参考 **[安装说明](https://babeljs.io/en/setup)**
## 其他安装方式
如果你没有使用模块管理工具或者包管理工具,也可以使用官方托管在 unpkg CDN 上的构建版本.只需在HTML文件底部添加以下`<script>`标签:
```html
<script src="https://unpkg.com/styled-components/dist/styled-components.min.js"></script>
```
添加 styled-components 之后就可以访问全局的 `window.styled` 变量.
```javascript
const Component = window.styled.div`
  color: red;
`
```
>注意
>
>这用使用方式需要页面在 styled-components script 之前引入 [react CDN bundles](https://reactjs.org/docs/cdn-links.html) 