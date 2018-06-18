From [freeCodeCamp](https://learn.freecodecamp.org/front-end-libraries/react)

- React uses a syntax extension of JavaScript called JSX. Because JSX is a syntactic extension of JavaScript, you can actually write JavaScript directly within JSX. To do this, you simply include the code you want to be treated as JavaScript within curly braces: `{ 'this is treated as JavaScript code' }`. However, because JSX is not valid JavaScript, JSX code must be compiled into JavaScript. The transpiler Babel is a popular tool for this process. 


- One important thing to know about nested JSX is that it must return a single element. Here's an example:

	Valid JSX:
	```
	const JSX = 
	<div>
	<p>Paragraph One</p>
	<p>Paragraph Two</p>
	<p>Paragraph Three</p>
	</div>
	```
	Invalid JSX:

	```
	const JSX = 
	<p>Paragraph One</p>
	<p>Paragraph Two</p>
	<p>Paragraph Three</p>
	```

- To put comments inside JSX, you use the syntax `{/* */}` to wrap around the comment text.

- So far, you've learned that JSX is a convenient tool to write readable HTML within JavaScript. With React, we can render this JSX directly to the HTML DOM using React's rendering API known as ReactDOM. ReactDOM offers a simple method to render React elements to the DOM which looks like this: `ReactDOM.render(componentToRender, targetNode)`, where the first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to. As you would expect, `ReactDOM.render()` must be called after the JSX element declarations, just like how you must declare variables before using them.