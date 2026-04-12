A JavaScript library for building interactive user interfaces

*Goal:* be more declarative, as opposed to imperative like JavaScript

##### Setup

`react` is the core package with universal interface
`react-dom` is the browser-specific rendered; some other stuff like React Native use other renderes

React usually goes with other tools that are not really needed but very convenient.

1. NPM and Yarn for package management;
2. Webpack and Vite for building sparse files together;
3. JSX to provide shorter syntax via HTML markup (not a module, but a syntax extension);
4. Babel to compile JSX and newer JavaScript features for older browsers.

##### Components

Reusable chunks as JavaScript functions.

- There are function and class components
- Must return markup (which is what `createElement` generates)

```ts title="createElement.ts"
const component = (props) => React.createElement(
	type: string | React.ComponentType,
	props?: object | null, 
	...children: any[]
)
```

A sample application.

```js title=App.js
const Pizza = (props) => {
	return React.createElement("div", {}, [
		React.createElement("h1", {}, props.name),
		React.createElement("p", {}, props.description),
	]);
};
	
const App = () => {
	return React.createElement("div", {}, [
		React.createElement("h1", {}, "Pixel Perfect Pizzas"),
		React.createElement(Pizza, props1),
		React.createElement(Pizza, props2),
		React.createElement(Pizza, props3),
	]);
};
		
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(React.createElement(App));
```

Notes:
- `reactDOM.createRoot` signals where we want to render our app.
- `createElement` is used both to define components and to render them.
- We should **always** `createElement` our components, never call them like a function, so React maintains *inversion of control* and *hook management*.

JSX  simplifies this syntax.

```jsx title=App.jsx
const Pizza = (props) => {
	return (
		<div className="pizza">
			<h1>{props.name}</h1>
			<p>{props.description}</p>
		</div>
	);
};

const App = () => {
	return (
		<div>
			<h1>Padre Gino's Pizza – Order Now</h1>
			<Pizza
				name="Pepperoni"
				description="Mozzarella Cheese, Pepperoni"
			/>
			<Pizza
				name="The Hawaiian Pizza"
				description="Sliced Ham, Pineapple, Mozzarella Cheese"
			/>
			<Pizza
				name="The Big Meat Pizza"
				description="Bacon, Pepperoni, Italian Sausage"
			/>
		</div>
	);
};

const container = document.getElementById("root");
const root = createRoot(container);
root.render(<App />);
```

- Component names must be capitalized. JSX understands lowercase as a web components and not React components.
- Even self-contained components must contain the closing tag `\>` in JSX.
- `class` is substituted for `className` since `class` is a JS reserved keyword.
- `for` is substituted for `htmlFor` for the same reason.

**Default and named exports**

```jsx title=Pizza.jsx
export const Pizza = (props) => {
...
}

import { Pizza } from "./Pizza";

// Versus

const Pizza = (props) => {
...
}

export default Pizza;

import Pizza from "./Pizza";
```

##### Vite

We need to add module to the script tag so that the browser knows it's working with modern browser technology that allows you in development mode to use modules directly.

```html title=index.html
<script type="module" src="./src/App.js"></script>
```

Vite also needs a settings file.

```js title=vite.config.js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({ plugins: [react()], });
```

## Hooks

Hooks introduce interactivity and side effects in React components.
Components should <mark style="background: #ADCCFFA6;">always</mark> produce consistent markup given the same input!

> Hooks must be called in the same order every time, must not be inside loops, functions, or other control structures.


`useState`

```jsx title=state.jsx
[name, setName] = useState(default_value);
```

*Two-way data binding:*  React will not automatically update components unless there is state management happening there.

