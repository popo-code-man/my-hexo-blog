---
title: useContext模拟redux
date: 2022-04-02 22:58:49
tags: react
categories: react
cover: react-logo.png
top_img: react-logo.png
---

# useContext 模拟 redux

## 前言

虽然 Redux 是 React 生态系统中广泛使用的状态管理工具，但它具有一定的复杂性和学习曲线。在一些小型项目中，Redux 可能会增加不必要的复杂性，因此可以使用 useContext 模拟 Redux 的功能。useContext 是 React 提供的一种访问全局状态的方式，可以使组件轻松地访问全局状态。通过模拟 Redux 的功能，可以使用更简单的方式来管理全局状态，并减少使用 Redux 所需的代码量和依赖项。

此外，使用 useContext 模拟 Redux 还可以提高应用程序的性能。Redux 的工作流程包括将状态更新分发给所有订阅该状态的组件。这种方式在大型应用程序中非常有用，但在小型应用程序中可能会降低性能。而使用 useContext 模拟 Redux 可以直接将全局状态传递给需要访问的组件，减少了 Redux 的中间件和依赖项的使用，从而提高了应用程序的性能。

综上所述，使用 useContext 模拟 Redux 可以在小型项目中提供更简单和高效的状态管理方案，并降低了使用 Redux 的学习曲线和复杂性。

## 实现过程

`useContext`用于获取全局状态，而`useReducer`用于管理全局状态的变化。具体实现如下：

1. 创建一个`context`对象，该对象将充当全局状态的容器。可以使用`React.createContext`函数创建一个新的`context`对象：

```javascript
const AppContext = React.createContext();
```

2. 在 App 组件中，将全局状态存储在`context`对象中。可以使用`useReducer`钩子来创建状态和更新函数

```javascript
function reducer(state, action) {
	switch (action.type) {
		case "increment":
			return { counter: state.counter + 1 };
		case "decrement":
			return { counter: state.counter - 1 };
		default:
			throw new Error();
	}
}

function App() {
	const [state, dispatch] = useReducer(reducer, { counter: 0 });

	return (
		<AppContext.Provider value={{ state, dispatch }}>
			<div>
				<h1>Counter: {state.counter}</h1>
				<button onClick={() => dispatch({ type: "increment" })}>
					Increment
				</button>
				<button onClick={() => dispatch({ type: "decrement" })}>
					Decrement
				</button>
			</div>
		</AppContext.Provider>
	);
}
```

3. 在需要访问全局状态的组件中，使用 useContext 来获取 context 对象并获取全局状态：

```javascript
function Counter() {
	const { state, dispatch } = useContext(AppContext);

	return (
		<div>
			<h1>Counter: {state.counter}</h1>
			<button onClick={() => dispatch({ type: "increment" })}>Increment</button>
			<button onClick={() => dispatch({ type: "decrement" })}>Decrement</button>
		</div>
	);
}
```


通过这种方式，可以将全局状态传递给任意数量的子组件，并且在需要访问全局状态的组件中可以轻松获取并更新该状态。此方法可以在一些小型项目中使用，并提供了一种基于useContext和useReducer的简单Redux实现。