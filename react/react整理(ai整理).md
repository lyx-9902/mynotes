# react整理

User: 总结react 知识点
Kimi: 我来为您系统总结 React 的核心知识点：

## 一、React 基础概念

### 1. 核心特点
- **组件化**：UI 拆分为独立、可复用的组件
- **声明式编程**：描述"UI 应该是什么样子"，而非"如何更新"
- **单向数据流**：数据自上而下传递（props），状态提升管理
- **虚拟 DOM**：通过 Diff 算法高效更新真实 DOM

### 2. JSX 语法
```jsx
// JSX 是 JavaScript 的语法扩展
const element = <h1 className="title">Hello React</h1>;

// 本质等价于
const element = React.createElement('h1', {className: 'title'}, 'Hello React');
```

## 二、组件类型

### 1. 函数组件（推荐）
```jsx
// 基础函数组件
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}

// 使用 Hooks 的状态管理
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

### 2. 类组件（较少使用）
```jsx
import { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## 三、核心 Hooks

| Hook          | 用途              | 示例                                          |
| ------------- | ----------------- | --------------------------------------------- |
| `useState`    | 状态管理          | `const [state, setState] = useState(initial)` |
| `useEffect`   | 副作用处理        | 数据获取、订阅、手动 DOM 操作                 |
| `useContext`  | 上下文消费        | 跨组件传递数据，避免 prop drilling            |
| `useRef`      | 引用 DOM/持久化值 | `const ref = useRef(initial)`                 |
| `useMemo`     | 缓存计算值        | 性能优化，避免重复计算                        |
| `useCallback` | 缓存函数引用      | 配合 React.memo 使用                          |
| `useReducer`  | 复杂状态逻辑      | 类似 Redux 的 reducer 模式                    |

### useEffect 详解
```jsx
useEffect(() => {
  // 执行副作用
  const subscription = props.source.subscribe();
  
  // 清理函数（可选）
  return () => {
    subscription.unsubscribe();
  };
}, [dependency1, dependency2]); // 依赖数组
```

## 四、组件通信

### 1. Props 传递（父子组件）
```jsx
// 父组件
function Parent() {
  const [data, setData] = useState('');
  return <Child data={data} onChange={setData} />;
}

// 子组件
function Child({ data, onChange }) {
  return <input value={data} onChange={e => onChange(e.target.value)} />;
}
```

### 2. Context API（跨层级）
```jsx
const ThemeContext = createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  const theme = useContext(ThemeContext);
  return <div>Current theme: {theme}</div>;
}
```

### 3. 状态管理方案
- **Local State**: `useState`, `useReducer`
- **Global State**: Context API, Redux, Zustand, Jotai, Recoil

## 五、性能优化

| 技术                | 使用场景                                   |
| ------------------- | ------------------------------------------ |
| `React.memo`        | 组件 props 不变时跳过渲染                  |
| `useMemo`           | 缓存昂贵的计算结果                         |
| `useCallback`       | 缓存事件处理函数，避免子组件不必要的重渲染 |
| `lazy` + `Suspense` | 代码分割，按需加载组件                     |
| `key` 属性          | 列表渲染时帮助 React 识别元素              |

```jsx
// React.memo 示例
const MemoizedComponent = React.memo(function MyComponent({ data }) {
  return <div>{data}</div>;
});

// 配合 useCallback
function Parent() {
  const [count, setCount] = useState(0);
  
  const handleClick = useCallback(() => {
    console.log('clicked');
  }, []); // 空依赖，引用不变
  
  return <MemoizedComponent onClick={handleClick} />;
}
```

## 六、高级特性

### 1. 代码分割
```jsx
import { lazy, Suspense } from 'react';

const OtherComponent = lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <OtherComponent />
    </Suspense>
  );
}
```

### 2. Portals（传送门）
```jsx
import { createPortal } from 'react-dom';

function Modal({ children }) {
  return createPortal(
    children,
    document.getElementById('modal-root')
  );
}
```

### 3. Refs 转发
```jsx
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// 父组件中使用
const ref = useRef();
<FancyButton ref={ref}>Click me!</FancyButton>
```

### 4. Error Boundaries（错误边界）
```jsx
class ErrorBoundary extends Component {
  state = { hasError: false };
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    logErrorToMyService(error, errorInfo);
  }
  
  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}
```

## 七、React 18 新特性

| 特性              | 说明                                                |
| ----------------- | --------------------------------------------------- |
| **并发渲染**      | 可中断的渲染，提升用户体验                          |
| **自动批处理**    | 自动合并多个状态更新                                |
| **Suspense 改进** | 支持数据获取场景                                    |
| **Transitions**   | `useTransition` 区分紧急/非紧急更新                 |
| **新的 Hooks**    | `useId`, `useDeferredValue`, `useSyncExternalStore` |

```jsx
// useTransition 示例
import { useTransition } from 'react';

function TabContainer() {
  const [isPending, startTransition] = useTransition();
  const [tab, setTab] = useState('home');
  
  function selectTab(nextTab) {
    startTransition(() => {
      setTab(nextTab); // 非紧急更新
    });
  }
  
  return (
    <>
      {isPending && <Spinner />}
      <TabButton onClick={() => selectTab('home')}>Home</TabButton>
      {tab === 'home' && <Home />}
    </>
  );
}
```

## 八、常用模式

### 1. 受控 vs 非受控组件
```jsx
// 受控组件
function ControlledInput() {
  const [value, setValue] = useState('');
  return <input value={value} onChange={e => setValue(e.target.value)} />;
}

// 非受控组件
function UncontrolledInput() {
  const inputRef = useRef(null);
  return <input ref={inputRef} defaultValue="initial" />;
}
```

### 2. 自定义 Hooks
```jsx
function useWindowSize() {
  const [size, setSize] = useState({ width: 0, height: 0 });
  
  useEffect(() => {
    const updateSize = () => {
      setSize({ width: window.innerWidth, height: window.innerHeight });
    };
    window.addEventListener('resize', updateSize);
    updateSize();
    return () => window.removeEventListener('resize', updateSize);
  }, []);
  
  return size;
}
```

## 九、生态系统

| 类别       | 常用库                                       |
| ---------- | -------------------------------------------- |
| 路由       | React Router                                 |
| 状态管理   | Redux Toolkit, Zustand, Jotai                |
| 表单处理   | React Hook Form, Formik                      |
| 样式方案   | CSS Modules, Styled-components, Tailwind CSS |
| 测试       | Jest, React Testing Library, Cypress         |
| 服务端渲染 | Next.js, Remix                               |
| 动画       | Framer Motion, React Spring                  |

---

**学习建议**：
1. 先掌握函数组件 + Hooks 的核心用法
2. 理解数据流和组件通信机制
3. 逐步学习性能优化技巧
4. 结合实际项目（如 Next.js）深入实践

需要我针对某个具体知识点展开详细讲解吗？

