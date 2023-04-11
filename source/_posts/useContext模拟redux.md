---
title: useContext模拟redux
date: 2022-08-02 22:58:49
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


```typeScript
import React, { createContext, useContext, useReducer } from 'react';

// 创建一个全局的Context
interface IState {
  count: number;
}

type ActionType = { type: 'INCREMENT' } | { type: 'DECREMENT' };

interface IContextProps {
  state: IState;
  dispatch: React.Dispatch<ActionType>;
}

const MyContext = createContext({} as IContextProps);

// 创建一个reducer函数
const reducer = (state: IState, action: ActionType) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
};

// 创建一个Provider组件，用于提供全局的状态和操作函数
const MyProvider: React.FC = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <MyContext.Provider value={{ state, dispatch }}>
      {children}
    </MyContext.Provider>
  );
};

// 创建一个自定义Hook，用于在组件中访问全局的状态和操作函数
const useMyContext = () => {
  const { state, dispatch } = useContext(MyContext);
  return [state, dispatch] as const;
};

// 在组件中使用自定义Hook
const Counter: React.FC = () => {
  const [state, dispatch] = useMyContext();

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
    </div>
  );
};

// 使用MyProvider组件包裹App组件，使得全局的状态可以在组件中访问
const App: React.FC = () => {
  return (
    <MyProvider>
      <Counter />
    </MyProvider>
  );
};

```




通过这种方式，可以将全局状态传递给任意数量的子组件，并且在需要访问全局状态的组件中可以轻松获取并更新该状态。此方法可以在一些小型项目中使用，并提供了一种基于useContext和useReducer的简单Redux实现。