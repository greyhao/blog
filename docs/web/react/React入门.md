## React 入门

### 一. 前提

需要环境：Node >= 14.0.0 && npm >= 5.6



### 二. 创建工程

`# npm create-react-app my-react-app`  // 执行需要时间

// 使用 TypeScript

`# npx create-react-app my-react-app --template typescript`



### 三. 运行项目

`# cd my-react-app`

`# npm start` // 启动服务，并且会自动打开浏览器标签（并且当文件有修改时会自动刷新显示）



### 四、语法

JSX 是在 JavaScript 语法上的拓展，HTML 代码和 JSX 可以共存。

```react
const heading = <h1>Hello React!</h1>
```

heading 常量成为 JSX 表达式。

浏览器无法读取直接解析 JSX ，使用 Bable 或 Parcel 之类的工具编译，上面的代码编译之后的样子：

```react
const header = React.createElement("h1", null, "Hello React!");
```

编译过程不需自行配置。



#### 变量

在 JSX 中使用： {xx} 来识别变量

```react
// 定义变量
const name = "React";

// 使用变量
<p>hello {name}!</p>
```



####处理事件

在 JSX 中添加事件处理逻辑

```react
<button
  type="button"
  onClick={() => alert("hi!")}
>
  Say hi!
</button>
```





#### 定义组件



函数组件；类组件；

当组件中只包含一个 render 方法，并且不包含 state，那么使用函数组件。



**组件名首字母大写。**



**无论是什么组件，都不能修改自身的 props。**

**所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。**



在定义组件时使用 `<React.fragment>` 包裹多个标签，不会添加额外节点。短语法是 `<></>`，显式 `<React.fragment>` 语法声明的片段可能有 key，key 是唯一可以传递给 fragment 的属性。



this.props 和 this.state 可能会异步更新，不依赖他们的值更新下一个状态。



##### 1. 简单函数组件

```react
// Text.js 
// 显示一句文本
function Text() {
  return (
    <div>
      <p>Hello Widget!</p>
    </div>
  );
}

export default Text;

// 在 App.js 中使用
import Text from "./Text";

// 使用
<Text></Text>
```



##### 2. 带属性的函数组件

将数据传递给组件

```react
// Text.js 
// 显示一句文本
function Text(props) {
  // 获取传入的属性名为 name 的值
  const name = props.name;
  return (
    <div>
      <p>Hello {name}!</p>
    </div>
  );
}
// export 供其他组件使用
export default Text;


// 在 App.js 中使用，先 import
import Text from "./Text";

// 使用 设置属性 name 的值
<Text name="React"></Text>
```



##### 3. 函数组件间的交互（数据传递）

组件中的数据给到被引用处

```react
// Text.js
// 点击时回传数据
export default function Text(props) {
  function clickBtn(e){
    e.preventDefault();
    props.showInfo("Say Hello!");
  }
  return(
    <div>
      <button onClick={clickBtn}></button>
    </div>
  );
}


// App.js
// 定义回调方法
function showInfo(msg) {
  alert(msg);
}

// 传入回调方法
<Text showInfo={showInfo}></Text>
```



##### 4. State 和 useState

组件自身拥有的数据成为状态（State），状态可以被更新。

hooks ：为组件提供新功能的方法，例如 state。

`useState` 为组件创建状态变量，定义的时候设置变量的初始值。该方法返回一个状态和改变状态的方法。



```react
import {useState} from "react";

// name 初始值为 ""
const [name, setName] = useState("");

// 接下来可以使用 name 获取具体的值， 使用 setName(xx) 更新 name 的值
```



##### 5. 类组件，并传递数据

```react
// List.js 定义组件
import React from "react";

class List extends React.Component {
  
  // 构造方法
  constructor(props) {
    // 构造方法中必须调用
    super(props);
    // 定义 statue 的变量
    this.state = {
      name: "";
    };
	}
  
  handlerClick(msg) {
    // 更新 statue 中变量的值
    this.setState({name: msg})
  }
  
  render(){
    return(
      <div>
        // 使用 state 中的变量
        <h1>List for {this.state.name}</h1>
        <ul>
          <li onClick={()=> {
              this.handlerClick('A');
            }}>A</li>
          <li onClick={function() {
              console.log('click li - B');
            }}>{this.props.name}</li> // 使用传入进来的 name 变量
          <li>C</li>
        </ul>
      </div>
    );
  }
}

// app.js 使用组件
import List from "./List";

// 使用
<List name="Chars"></List>
```



##### 6. 事件处理

**必须显式使用 preventDefault 阻止默认行为**



处理事件方法定义及使用方式：

```react
// 绑定方法
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isToggleOn: true };
    // 此时绑定必不可少
    this.handleClick = this.handleClick.bind(this);
  }
  
  handleClick {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

	render(
  	return(
    	// 调用事件处理
    	<button onClick={this.handleClick}>
      	{this.state.isToggleOn ? "ON" : "OFF"}
    	</button>
  	);
  );
}

// 不用绑定的方式 方式一
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isToggleOn: true };
  }
  
  // 定义方法方式修改
  handleClick = () => {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

	render(
  	return(
    	// 调用事件处理
    	<button onClick={this.handleClick}>
      	{this.state.isToggleOn ? "ON" : "OFF"}
    	</button>
  	);
  );
}

// 不用绑定的方式 方式二
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isToggleOn: true };
  }
  
  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

	render(
  	return(
    	// 调用方法方式修改，使用箭头函数
    	<button onClick={() => this.handleClick()}>
      	{this.state.isToggleOn ? "ON" : "OFF"}
    	</button>
  	);
  );
}

```



向事件处理程序传递参数

```react
// 以下两种方式等价

// 使用箭头函数
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>

// 使用 bind 方式
<button onClick={this.deleteRow(this, id)}>Delete Row</button>
```



#####7. 条件渲染

可以使用 if...else、&&、三目运算符

```react
// if...else
function ShowInfo(props) {
  if(props.count > 1) {
    return <h1>have {props.count} messages.</h1>
  } else {
    return <h1>have {props.count} message.</h1>
  }
}


// &&  
// true && expression 总是会返回 expression, 而 false && expression 总是会返回 false
// 当 count > 1 会显示 h2 标签
function ShowInfo(props) {
  return (
    <div>
      <h1>Hello!</h1>
      {props.count > 1 && <h2>have {props.count} messages.</h2>}
    </div>
  );
}


// 三目运算符 condition ? true : false;
function ShowInfo(props) {
  return (
    <div>
      <h1>Hello! {props.count}{props.count > 1 ? " messages" : " message"} </h1>
    </div>
  );
}


// 隐藏组件，通过 return null 实现，返回 null 不会影响组件的生命周期
function ShowInfo(props) {
  if(props.hidden) {
      return null;
  }
  return <h1>show info</h1>;
}
```



##### 8. 列表

**在 `map()` 方法中的元素需要设置 key 属性**

**key 值在兄弟节点之间必须唯一**



```react
// 定义 
// 使用 map 
function NumberList(props) {
  let numbers = props.numbers;
  const number = numbers.map((number) =>
      <li key={number.toString()}>{number}</li>
  );
  return <ul>{number}</ul>;
}

// 使用 forEach
function NumberList(props) {
  let numbers = props.numbers;
  const number = [];
  numbers.forEach((number) => {
  	number.push(<li key={number.toString()}>{number}</li>);  
	});
  return <ul>{number}</ul>;
}


// 使用
const numbers = [1, 2, 3, 4, 5];

<NumberList numbers={numbers}></NumberList>


```



##### 9. 受控组件

渲染表单的 React 组件还控制着用户输入过程中表单发生的操作，被 React 以这种方式控制取值的表单输入元素叫做受控组件。

监听 input 的 onChange 方法，将获取到的值设置给 state 中定义的对应变量。

**给受控组件知道 `value` 属性的值，会阻止更改输入，除非值为：null 或 undefined **



```react
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {article: "请撰写一篇关于你喜欢的 DOM 元素的文章", value: "lime"};
    
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  
  handleChange(event) {
    this.setState({article: event.target.value});
  }
  
  handleSubmit(event) {
    alert("submit name: " + this.state.article);
    event.preventDefault();
  }
  
  handleSelectChange(event) {
    this.setState({value: event.target.value});
  }
  
  render(){
    return(
      <form onSubmit={this.handleSubmit}>
        <label>
          name:
          <textarea value={this.state.article} onChange={this.handleChange}/>
          {// <input type="text" value={this.state.article} onChange={this.handleChange}/>
        }
        </label>
        
        // 设置默认选择项，监听选择变化
        // 多选设置 multiple={true}  value={['B', 'C']}
        <select value={this.state.value} onChange={this.handleSelectChange}>
              <option value="grapefruit">葡萄柚</option>
              <option value="lime">酸橙</option>
              <option value="coconut">椰子</option>
              <option value="mango">芒果</option>
            </select>
        
        <input type="submit" value="Submit"/>
      </form>
    );
  };
}
```



处理多个输入时

```react
handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      // 根据控件的 name 属性选择要执行的操作
      [name]: value
    });
}

// 控件定义

<form>
	<label>
		参与:
		<input
      // 设置 name 属性
			name="isGoing"
			type="checkbox"
			checked={this.state.isGoing}
			onChange={this.handleInputChange} />
		</label>
		<br />
		<label>
			来宾人数:
			<input
				name="numberOfGuests"
				type="number"
				value={this.state.numberOfGuests}
				onChange={this.handleInputChange} />
		</label>
</form>
```



##### 10. 组合

**组件可以接受任意 props ，包含基本数据类型、react 元素以及函数**

**props.children  标签中的所有子组件**



包含关系：

```react
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      // children 是指 FancyBorder 标签中的所有子控件 
      {props.children}
      <div>
        {props.content}
      </div>
    </div>
  );
}


function WelcomeDialog() {
  let contentDiv = <div>This is content!</div>;
  return (
    // content 传入的是一个控件
    <FancyBorder color="blue" content={contentDiv}>
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```



特例关系

```react
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

// WelcomeDialog 是 Dialog 的特殊实例
function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}
```



#### 高阶组件 （HOC）

高阶组件（HOC）是 React 中用于复用组件逻辑的一种高级技巧。HOC 自身不是 React API 的一部分，它是一种基于 React 的组合特性而形成的设计模式。

**高级组件是参数为组件，返回值为新组件的函数。**

```react
// 使用 withSubscription，参数 1 为组件，参数 2 为被监听的数据
const CommentListWithSubscription = withSubscription(
  CommentList,
  (DataSource) => DataSource.getComments()
);
```





#### 给控件设置焦点

```react
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // 定义 textInput 元素的 ref
    this.textInput = React.createRef();
  }
  
  render(){
    return(
    	<input
        type="text"
        ref={this.textInput}
      />
    );
  }
}

// 需要把焦点设置在该控件时
focus() {
  this.textInput.current.focus();
}
```



#### 动态导入 `React.lazy`

React.lazy 目前只支持默认导出（default exports）

```react
// 在首次渲染时，自动导入组件所在的包
const OtherComponent = React.lazy(() => import('./OtherComponent'));

// 使用
// fallback 设置加载过程中要展示的元素
<Suspense fallback={<div>Loading</div>}>
	<OtherComponent/>
</Suspense>

```



局部控件切换优化（标签切换）

```react
function handleTabSelect(tab) {
  // 调用该方法，优化切换时体验
	startTransition(() => {
    setTab(tab);
	})
}
```



#### Context

提供无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。

为全局数据时候使用 Context

```react
// 定义 App.js 
const ThemeContext = React.createContext("light");


// 使用 
import { ThemeContext } from "../App";

class Ctx extends React.Component {
  render() {
    return (
      // 设置 ThemeContext 的值
      <ThemeContext.Provider value="red">
        <Toolbar> </Toolbar>
      </ThemeContext.Provider>
    );
  }
}

function Toolbar() {
  return (
    <div>
      // 中间组件不需要设置 props
      <ThemedButton></ThemedButton>
    </div>
  );
}

class ThemedButton extends React.Component {
  // 指定 contextType 读取当前 ThemeContext 的值
  static contextType = ThemeContext;
  render() {
    return <button theme={this.context}>{this.context}</button>;
  }
}

```



#### Portals

Portal 提供了一种将子节点渲染到存在于父组件之外的 DOM 节点的优秀方案。

`ReactDOM.createPortal(child, container) // child 是任何可渲染的 React 子元素，container 是一个 DOM 元素 `

使用场景：对话框、悬浮卡以及提示框



#### Render Props

在组件之间使用一个值为函数的 prop 共享代码。

将一个组件的数据传递给另一个组件

```react
// 在组件 Mouse 的中定义
this.props.render(this.state);

// 使用组件
<Mouse render={mouse => (
    <Cat mouse={mouse}></Cat>
  )}>
</Mouse>
```





####生命周期方法

* componentDidMount() 挂载方法，组件第一次被渲染到 DOM 时调用
* componentWillUnmount() 卸载方法，当 DOM 中组件被删除时调用
* componentDidUpdate() 



//  错误边界（仅可以捕捉其子组件的错误），定义下面任意一个或两个方法

* static getDerivedStateFromError(error)  定义当抛出错误时，需要渲染的备用 UI
* componentDidCatch(error, errorInfo)  获取抛出的错误





#### Hook

Hook 是 React 16.8 的新增特性，可以在不编写 class 的情况下使用 state 以及其他的 React 特性。本质是 JavaScript 函数。

#####使用规则

* 只能在函数最外层调用，循环、判断及子函数中不要用（如果想有条件地执行一个 effect，可以将判断放到 Hook 的内部）
* 只能在 React 的函数组件中调用，不要在其他 JavaScript 函数中调用

可以使用 ESLint 插件来强制执行上面的规则

插件添加到项目中：

`npm install eslint-plugin-react-hooks --save-dev`

ESLint 配置

```json
{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    "react-hooks/rules-of-hooks": "error", // 检查 Hook 的规则
    "react-hooks/exhaustive-deps": "warn" // 检查 effect 的依赖
  }
}
```



#####hook 方法

* useState  状态值
* useEffect  
  * 同生命周期方法具有相同的用途：componentDidMount、componentDidUpdate、componentWillUnmount
  * 有 return 函数时，会在执行清除的时候调用这个函数
  * 每次更新都会运行
* useContext
* useReducer



单个组件可以使用多个 State Hook 和 Effect Hook，因为 Hook 的调用顺序每次都是相同的，所以每次渲染都是相同的。



```react
function Example() {
  // count 变量，初始值为 0；setCount 方法用来修改 count 的值
  const [count, setCount] = useState(0);

  // 组件更新、销毁、变更的时候都会执行方法中的代码
  // 第二个参数：[count] 是可选参数，是指只有 count 发生改变时才会重新渲染
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

// 有条件的执行 Effect Hook
useEffect(() => {
  if(name !== "") {
    localStorage.setItem('formData', name);
  }
});
```



#####自定义 Hook

自定义 Hook 是一个函数，其名称以 use 开头，函数内部可以调用其他的 Hook







### 五. npm 引用模块

####路由

安装 

 `npm install react-router-dom@6`

使用

```react
import ReactDOM from "react-dom/client";
import {
  BrowserRouter,
  Routes,
  Route,
} from "react-router-dom";
import App from "./App";
import Expenses from "./routes/expenses";
import Invoices from "./routes/invoices";

const root = ReactDOM.createRoot(
  document.getElementById("root")
);
root.render(
  // 使用路由
  <BrowserRouter>
    <Routes>
      // 定义所有路由
      <Route path="/" element={<App />} />
      <Route path="expenses" element={<Expenses />} />
      <Route path="invoices" element={<Invoices />} />
      // 嵌套路由，App 页面中只需要切换一部分  
      // App 中需要路由切换的部分添加 <Outlet />
      <Route path="/" element={<App />}>
        <Route path="expenses" element={<Expenses />} />
      	<Route path="invoices" element={<Invoices />} />
      </Route>
    </Routes>
  </BrowserRouter>
);
```

