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
从 npm 安装 styled-components 只需要一个命令:
```
npm install --save styled-components
```

>强烈推荐使用 styled-components 的 [babel 插件](https://www.styled-components.com/docs/tooling#babel-plugin) (当然这不是必须的).它提供了许多益处,比如更清晰的类名,SSR 兼容性,更小的包等等.

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

## 入门

`styled-components` 通过标记的模板字符来设置组件样式.

它移除了组件和样式之间的映射.当我们通过`styled-components`定义样式时,我们实际上是创建了一个附加了样式的常规 React 组件.

以下的例子创建了两个简单的附加了样式的组件, 一个`Wrapper`和一个`Title`:

```jsx
// 创建一个 Title 组件,它将渲染一个附加了样式的 <h1> 标签
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// 创建一个 Wrapper 组件,它将渲染一个附加了样式的 <section> 标签
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

// 就像使用常规 React 组件一样使用 Title 和 Wrapper 
render(
  <Wrapper>
    <Title>
      Hello World!
    </Title>
  </Wrapper>
);
```

>注意
>
> styled-components 会为我们自动创建 CSS 前缀

## 基于 props 的适配
我们可以将 props 以插值的方式传递给`styled component`,以调整组件样式.

下面这个 `Button` 组件持有一个可以改变`color`的`primary`属性. 将其设置为 ture 时,组件的`background-color`和`color`会交换.

```jsx
const Button = styled.button`
  /* Adapt the colors based on primary prop */
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

render(
  <div>
    <Button>Normal</Button>
    <Button primary>Primary</Button>
  </div>
);
```

## 样式继承
可能我们希望某个经常使用的组件,在特定场景下可以稍微更改其样式.当然我们可以通过 props 传递插值的方式来实现,但是对于某个只需要重载一次的样式来说这样做的成本还是有点高.

创建一个继承其它组件样式的新组件,最简单的方式就是用构造函数`styled()`包裹被继承的组件.下面的示例就是通过继承上一节创建的按钮从而实现一些颜色相关样式的扩展:

```jsx
// 上一节创建的没有插值的 Button 组件
const Button = styled.button`
  color: palevioletred;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

// 一个继承 Button 的新组件, 重载了一部分样式
const TomatoButton = styled(Button)`
  color: tomato;
  border-color: tomato;
`;

render(
  <div>
    <Button>Normal Button</Button>
    <TomatoButton>Tomato Button</TomatoButton>
  </div>
);
```

可以看到,新的`TomatoButton`仍然和`Button`类似,我们只是添加了两条规则.

In some cases you might want to change which tag or component a styled component renders.这在构建导航栏时很常见，例如导航栏中同时存在链接和按钮,但是它们的样式应该相同.

在这种情况下,我们也有替代办法(escape hatch). 我们可以使用多态 ["as" polymorphic prop](https://www.styled-components.com/docs/api#as-polymorphic-prop) 动态的在不改变样式的情况下改变元素:

```jsx
const Button = styled.button`
  display: inline-block;
  color: palevioletred;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

const TomatoButton = styled(Button)`
  color: tomato;
  border-color: tomato;
`;

render(
  <div>
    <Button>Normal Button</Button>
    <Button as="a" href="/">Link with Button styles</Button>
    <TomatoButton as="a" href="/">Link with Tomato Button styles</TomatoButton>
  </div>
);
```

这也完美适用于自定义组件:
```jsx
const Button = styled.button`
  display: inline-block;
  color: palevioletred;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

const ReversedButton = props => <button {...props} children={props.children.split('').reverse()} />

render(
  <div>
    <Button>Normal Button</Button>
    <Button as={ReversedButton}>Custom Button with Normal Button styles</Button>
  </div>
);
```

## 给任何组件添加样式(Styling any components)
`styled`方法适用于任何最终向 DOM 元素传递 `className` 属性的组件,当然也包括第三方组件.
> 注意
>
>在 react-native 中，请使用 style 而不是 className.

```jsx
// 下面是给 react-router-dom  Link 组件添加样式的示例
const Link = ({ className, children }) => (
  <a className={className}>
    {children}
  </a>
);

const StyledLink = styled(Link)`
  color: palevioletred;
  font-weight: bold;
`;

render(
  <div>
    <Link>Unstyled, boring Link</Link>
    <br />
    <StyledLink>Styled, exciting Link</StyledLink>
  </div>
);
```

>注意
>
>也可以传递标签给`styled()`, 比如:` styled("div")`. 实际上`styled.tagname`的方式就是 styled(tagname)`的别名.

## 传递 props
如果添加样式的目标是 DOM 元素 (如`styled.div`), `styled-components `会传递已知的 HTML 属性给 DOM. 如果是一个自定义的 React 组件 (如`styled(MyComponent)`), `styled-components` 会传递全部 `props`.

以下示例展示如何传递 Input 组件的 props 到已装载的 DOM 节点, as with React elements.

```jsx
// 创建一个给<input>标签添加若干样式的 Input 组件 
const Input = styled.input`
  padding: 0.5em;
  margin: 0.5em;
  color: ${props => props.inputColor || "palevioletred"};
  background: papayawhip;
  border: none;
  border-radius: 3px;
`;

// 渲染两个样式化的 text input,一个标准颜色,一个自定义颜色
render(
  <div>
    <Input defaultValue="@probablyup" type="text" />
    <Input defaultValue="@geelen" type="text" inputColor="rebeccapurple" />
  </div>
);
```

注意, `inputColor prop`并没有传递给 DOM, 但是`type`和`defaultValue` 都传递了. `styled-components`足够智能,会自动过滤掉所有非标准 attribute.

## Coming from CSS