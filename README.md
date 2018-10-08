# 基础
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