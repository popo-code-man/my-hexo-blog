---
title: React中的动态表单实现
date: 2022-04-02 22:58:49
tags: react
categories: react
cover: react-logo.png
top_img: react-logo.png
---

# React 中的动态表单实现

在 `React` 中，我们可以很容易地创建动态表单，以便用户可以输入和提交数据。本文将介绍如何在 `React` 中实现动态表单。

## 表单基础

在 `React` 中，我们使用 `HTML` 表单元素来收集和提交用户数据。以下是一个基本的 `React` 表单：

```jsx
import React, { useState } from "react";

function BasicForm() {
	const [name, setName] = useState("");
	const [email, setEmail] = useState("");
	const [message, setMessage] = useState("");

	const handleSubmit = (event) => {
		event.preventDefault();
		console.log(`Name: ${name}, Email: ${email}, Message: ${message}`);
	};

	return (
		<form onSubmit={handleSubmit}>
			<label>
				Name:
				<input
					type="text"
					value={name}
					onChange={(e) => setName(e.target.value)}
				/>
			</label>
			<label>
				Email:
				<input
					type="email"
					value={email}
					onChange={(e) => setEmail(e.target.value)}
				/>
			</label>
			<label>
				Message:
				<textarea
					value={message}
					onChange={(e) => setMessage(e.target.value)}
				/>
			</label>
			<button type="submit">Submit</button>
		</form>
	);
}
```

在这个例子中，我们使用 `useState` 钩子来创建三个状态变量，分别用于存储用户的名称、电子邮件和消息。在`<form>`元素上，我们使用 `onSubmit` 事件处理程序来处理表单提交事件。我们还使用`<label>`元素和各种表单元素来收集用户数据。

## 动态表单

现在，假设我们希望动态地添加和删除表单字段。例如，我们可能想要一个按钮来添加新的电子邮件输入框，以便用户可以添加多个电子邮件地址。以下是一个实现此功能的示例：

```jsx
import React, { useState } from "react";

function DynamicForm() {
	const [fields, setFields] = useState([{ value: "" }]);

	const handleAddField = () => {
		const values = [...fields];
		values.push({ value: "" });
		setFields(values);
	};

	const handleRemoveField = (index) => {
		const values = [...fields];
		values.splice(index, 1);
		setFields(values);
	};

	const handleSubmit = (event) => {
		event.preventDefault();
		console.log(fields);
	};

	const handleChange = (index, event) => {
		const values = [...fields];
		values[index].value = event.target.value;
		setFields(values);
	};

	return (
		<form onSubmit={handleSubmit}>
			{fields.map((field, index) => (
				<div key={index}>
					<label>
						Email:
						<input
							type="email"
							value={field.value}
							onChange={(e) => handleChange(index, e)}
						/>
					</label>
					{fields.length > 1 && (
						<button type="button" onClick={() => handleRemoveField(index)}>
							Remove
						</button>
					)}
				</div>
			))}
			<button type="button" onClick={handleAddField}>
				Add Email
			</button>
			<button type="submit">Submit</button>
		</form>
	);
}
```

在这个例子中，我们使用 `useState` 钩子创建了一个名为 `fields` 的状态变量，它是一个数组，每个元素都是一个对象，其中包含一个名为 `value` 的属性。在表单渲染时，我们使用 `map` 函数迭代 `fields` 数组，并为每个元素渲染一个电子邮件输入框和一个删除按钮。当用户单击“添加电子邮件”按钮时，我们将一个新的`{ value: '' }`对象推入 `fields` 数组中。当用户单击删除按钮时，我们使用 `splice` 函数从 `fields` 数组中删除相应的元素。

我们还添加了 `handleChange` 事件处理程序，它根据用户输入更新 `fields` 状态变量中的相应值。最后，我们将 `fields` 数组传递给 console.log 函数，以便在提交表单时显示用户输入的所有电子邮件地址。
