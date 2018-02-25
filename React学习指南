# React学习指南
## 目录
- [前言]()
- [React入门经典]()
  - [JSX简介]()
  - [元素渲染]()
  - [组件和属性]()
  - [状态和生命周期]()
## 前言
> react是一个目前非常火热的前端框架，即使前一阵子因为开源证书问题被推到了风口浪尖，但是仍然没有浇灭广大开发者对其的热情。另一方面公司内部也正在有angular转向react，我也就很(bu)高(de)兴（yi）地去学习这个技术了。（PS：很惊讶也很佩服大FE们所构建的Angular转React step on step改造之路）

## React入门经典
> 说是入门经典，实际上也是从各个地方拼凑起来的教程。   

技术版本：
1. node: v6.7.0
2. npm: 3.10.3
3. 安装create-react-app: npm intall -g create-react-app。
4. 安装第一个app
```
create-react-app my-app
cd my-app
npm start
浏览器输入：localhost:3000就可以看到了。
```
### JSX简介
> JSX的介绍可以看[这里](https://reactjs.org/docs/introducing-jsx.html)。
#### 在JSX中嵌入表达式
```
function getFullName(user) {
  return user.firstName + ' ' + user.lastName;
};

const user = {
  firstName: 'liang',
  lastName: 'li'
};

const ele = (
  <h1>
    Hello, {getFullName(user)}!
  </h1>
);
    
ReactDOM.render(
  ele,
  document.getElementById('root')
);
```
#### JSX本身也是一种语法
> 因此你也可以这样使用
```
function getFullName(user) {
  return user.firstName + ' ' + user.lastName;
};

const user = null;

function getEle(user) {
  if (user) {
      return <h1>Hello, {getFullName(user)}!</h1>;
  }
  return <h1>Hello, Stranger!</h1>;
}
    
ReactDOM.render(
  getEle(user),
  document.getElementById('root')
);
```
上面的例子中，user变量设为了null，ReactDOM.render方法的元素使用方法调用来获取了。

#### 指定属性
直接使用字符串值作为属性值
```
const element = (
  <input tabIndex="0" value="tab键第一个获取焦点的标签" />
);
```
使用花括号引入js表达式作为属性值

```
const user = {
  avatarUrl: '头像.png'  
};
const element = (
  <img src={user.avatarUrl} />
);
```
> 这里需要注意，千万不能引号和花括号一起使用，例如
``<img src="{user.avatarUrl}" />``

##### 重要说明
Since JSX is closer to JavaScript than to HTML, React DOM uses camelCase property naming convention instead of HTML attribute names.

For example, class becomes className in JSX, and tabindex becomes tabIndex.

#### 指定子元素
```
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

#### JSX可以防止注入攻击
```
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```
React DOM在渲染值之前会将其转义成字符串，因此可以防止注入攻击（XSS, cross-site-scripting）。

### 元素渲染
> 元素是React应用的最小构筑单元。

元素描述你能够在浏览器上看到的东西。

不同于浏览器DOM元素，React元素是一个简单的对象，并且创建的成本很低。React DOM能够够更新DOM以匹配React元素。

#### 在DOM上渲染元素。
先定义一个div
```
<div id="root"></div>
```
仅由React构筑的应用程序只有单一的root DOM节点。如果你想在应用中引入其他的React组件，那么需要给他提供单独的root DOM节点。

想要在root DOM节点中渲染React元素，需要将两者（root DOM节点和React元素）传入到``ReactDOM.render()``中，例如：
```
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

#### 更新已渲染的元素
React元素具有==不可变==性，一旦元素被创建，其子元素和属性将不可改变。元素就像是电影中的一帧。

就目前为止，更新UI的唯一方法就是创建一个新的元素并且将其传入到``ReactDOM.render()``。

例如一个时钟的例子：
```
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

#### React只做有必要的更新
React DOM会比较元素两次变化之间不同的部分，并对其进行更新。

在上面的那个例子里，使用浏览器的检查元素可以发现只有时间的文本部分在更新，其他的DOM元素并不会发生更新。

### 组件和属性
组件能够将UI独立、可复用化。

从概念上来说，组件像是js方法，能够接受任意的输入（属性）并且返回需要展示的React元素。

#### 方法和类组件
最简单的创建组件的方式是使用js方法：
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
上述的方法是一个合法的React组件，是因为他接受单一『props』对象参数并且返回一个React元素。由于其像js方法，因此称为方法组件。

也可以使用ES6中的类来定义一个组件：
```
class Welcome extends React.Component {
  render() {
      return <h1>Hello, {this.props.name}</h1>;
  }
}
```

#### 组件渲染
在之前的例子中，我们只使用React元素来表示一个DOM标签：
```
const element = <div />;
```
然而，元素也也可以代表用户定义的组件：
```
const element = <Welcome name="Sara" />;
```
当使用组件方式时，JSX属性会作为对象传入到组件中，我们称之为『props』。
例如：
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="leon" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
我们来看一下上面的整个过程：
1. 我们调用了``ReactDOM.render()``方法来渲染``<Welcome name="leon">``元素。
2. React使用``{name: 'leon'}``属性去调用了``Welcome元``素。
3. 组件``Welcome``返回了``<h1>Hello, leon</h1>``。
4. React DOM高效地更新了DOM节点以匹配``<h1>Hello, leon</h1>``。

#### 复合组件
组件可以作为其他组件的输出。例如，App组件多次渲染的Welcome组件：
```
function Welcome(props) {
  return (
    <h1>Hello, {props.name}</h1>
  );
}
function App() {
  return (
    <div>
      <Welcome name="leon" />
      <Welcome name="laoyao" />
      <Welcome name="sunxu" />
    </div>
  );
}
ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

#### 组件抽离
要乐衷于将组件分割成更小的组件。

例如一个评论组件：
```
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
首先可以将头像抽离成组件。

然后将用户信息抽离成组件，其中包含头像组件。
```
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />

  );
}
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

#### 属性是只读的
无论是用方法还是类来声明组件，它的属性都不应该被修改。例如一个求和的方法：
```
function sum(a, b) {
  return a + b;
}
}
```
这个方法被称为是『单纯的』（也就是纯函数），因为他并没有试图去改变传入的值。并且只要输入相同，那么输出也是相同的。

与之对应的就是非纯函数，这是因为他改变了输入参数：
```
function withdraw(account, amount) {
  account.total -= amount;
}
```
React充满灵活性，但是也有一个严厉的规则：
> 所有的React组件都应当是一个纯函数，其属性不能改变。

诚然，应用程序是动态的并且时刻都在改变。因此，React中引入了一个新的观点，也就是『state』。state允许React改变其输出来响应与用户的交互行为、网络应答或者其他的一些交互，这样就不会破坏其规则了。

### 状态和生命周期
到目前为止只介绍了一种更新元素的方式。

我们调用了ReactDOM.render()方法来更新已经渲染的元素：
```
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```
现在，我们将其改造称Clock组件来达到可复用和封装性的目的。
```
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```
上述例子缺少了一个重点：时间组件每秒更新应该是Clock组件内部的事情，然而例子中的时间是通过属性的方式传递到Clock组件中的！

理想状态的时间组件应该是类似这样的：
```
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
由于React的规则中属性是不可改变的，因此为了实现上述需求，需要在Clock组件中引入『state』。

> state和props类似，不同点在于state是组件私有的！

在之前我们介绍了组件也可以通过类来定义，类定义的组件比方法组件有更多的特征，其中之一就是state。也就是说，state是类组件特有的。

#### 将方法组件转换成类组件
转换5部曲：
1. 创建一个ES6类，继承React.Component，名字和方法组件同名。
2. 添加一个空的render()方法。
3. 将方法组件的内容移动到步骤2中的render()方法中。
4. 在移动后的render方法中，将``props``替换成``this.props``。
5. 删除原来的方法组件。
```
class Clock extends React.Component {
  render() {
      return (
        <div>
          <h1>Hello, world!</h1>
          <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
        </div>
      );
  }
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```
现在Clock组件就是通过类的方式定义了，这样就可以使用local state和生命周期 hooks了。

#### 添加Local State到类组件中
接下来，我们将``date``从props中移动到state中，这个过程需要三个步骤：
1. 将render方法中的``this.props.date``改成``this.state.date``。
```
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.
      </div>
    );
  }
}
```
2. 类中添加构造方法来初始化state。
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.
      </div>
    );
  }
}
```
注意props被传递到了构造方法中。
3. 移除``<Clock />``元素中的``date``属性
```
ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
最后的结果就是这样：
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```
接下来，我们需要让``Clock``自己进行更新，这需要生命周期钩子来实现。

#### 添加生命周期方法到类组件中
在大部分组件中，组件销毁时的==资源释放==是非常重要的！

我们需要在``Clock``组件第一次渲染的时候设置一个时间，这时候需要用到『mounting』（挂载）。

我们也需要在``Clock``组件移除的时候销毁这个时间，这时候我们需要『unmounting』（解除挂载）。

我们可以定义一些方法，让类组件在挂载和解除挂载的时候调用:
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {

  }

  componentWillUnmount() {

  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
这两个方法叫做『生命周期钩子』。

``componentDidMount()``钩子会在组件输出内容被渲染到DOM元素之后调用。因此比较适合用来设置一个时间：
```
componentDidMount() {
  this.timerID = setInterval(
    () => this.tick(),
    1000
  );
}
```
> 如果你不想在render方法中使用某个东西，那么它也不应该出现在state中。

在组件解除挂载时，我们需要释放更新时间的定时任务：
```
componentWillUnmount() {
  clearInterval(this.timerID);
}
```
接下来使用``this.setState()``来更新时间值：
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
  
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
  
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
  
  tick() {
    this.setState({
      date: new Date()
    });
  }
  
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
现在我们来看一下上述例子的过程：
1. 当``<Clock />``传入到``ReactDOM.render()``时，React会调用``Clock``组件的构造器。由于``Clock``需要展示当前时间，因此构造器中初始化了``this.state``属性，并且将时间传入其中。之后我们会更新state。
2. React接着调用``Clocl``组件的``render()``方法。这个方法返回的就是需要在浏览器展示的内容。接着React就会更新DOM元素使其于render输出的内容一直。
3. 当``Clock``组件输出的内容渲染到DOM后，React就会调用``componentDidMount()``方法。这个方法会通知浏览器启动一个定时任务以每秒调用一次组件的``tick()``方法。
4. 浏览器每秒调用一次``tick()``方法，该方法会将最新的时间通过``setState()``方法更新到state中，这时React就会知道state被更新过了，接着React就会调用``render()``方法来重新输出一个新的结果，最后更新DOM元素。
5. 如果``Clock``组件被DOM元素移除，React会调用``componentWillUnmonut()``方法来停止定时任务。

#### 正确使用State
##### 不要直接修改state
==这是错误的使用方式：==
```
this.state.comment = 'Hello';
```
请使用正确的方式：
```
this.setState({comment: 'Hello'});
```
> 只有在构造器中才能使用``this.state``

##### 可以异步更新state
由于``this.props``和``this.state``可以异步更新，因此不应该使用两者的值来计算新的state。

例如，接下来这个例子就可能更新错误：
```
this.setState({
  counter: this.state.counter + this.props.increment,
});
```
为了解决伤处的问题，``setState()``也可以接受一个方法。该方法可以接收``this.state.counter``和``this.props.increment``的值作为参数：
```
this.setState((prevState, props) => ({counter: prevState.counter + props.increment}));
```
上述例子中使用了[箭头函数](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)，当然也可以使用正常的函数：
```
this.setState(function(prevState, props) {
  return {
    counter: prevState.counter + props.increment
  };
});
```

##### state以合并的方式进行更新
当你调用``setState()``方法的时候，React将会把你传入的对象和当前对象进行合并。

例如，你的state可能包含许多独立的值：
```
constructor(props) {
  super(props);
  this.state = {
    posts: [],
    comments: []
  };
}
```
你可以通过分别调用``setState()``来独立地更新其中的属性：
```
componentDidMount() {
  fetchPosts().then(response => {
    this.setState({
      posts: response.posts
    });
  });
  fetchComments().then(response => {
    this.setState({
      comments: response.comments
    });
  });
}
```
这是一个简化版的例子，``this.setState({comments})``能够完整的保留``this.state.posts``，但是会完全覆盖``this.state.comments``。
