# 基础

## 动机

**styled-components是我们对于如何增强 React 组件中 CSS 表现这个问题的思考结果**
通过聚焦于单个用例,我们设法优化了开发者的体验和面向终端用户的输出.

除了提升开发者体验外, styled-components 同时提供以下特性:

- **Automatic critical CSS:** styled-components 持续跟踪页面上渲染的组件,并向自动其注入且仅注入样式. 结合使用代码拆分, 可以实现仅加载所需的最少代码.
- **解决了 class name 冲突:** styled-components 为样式生成唯一的 class name. 开发者不必再担心 class name 重复,覆盖和拼写错误的问题.
- **CSS 更容易移除:** 想要确切的知道代码中某个 class 在哪儿用到是很困难的. 使用 styled-components 则很轻松, 因为每个样式都有其关联的组件. 如果检测到某个组件未使用并且被删除,则其所有的样式也都被删除.
- **简单的动态样式:** 可以很简单直观的实现根据组件的 props 或者全局主题适配样式,无需手动管理数十个 classes.
- **无痛维护:** 
无需搜索不同的文件来查找影响组件的样式.无论代码多庞大，维护起来都是小菜一碟。
- **自动提供前缀:** 按照当前标准写 CSS,其余的交给 styled-components handle 处理.

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