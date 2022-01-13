
## Custom Elements

```javascript
class MyComponent extends HTMLElement {
	connectedCallback() { 
		this.innerHTML = `<h1>Hello world</h1>`; 
	} 
} 
customElements.define('my-component', MyComponent);
```

As the name implies, **custom elements** are HTML elements, like `<div>`, `<section>` or `<article>`, but something we can name ourselves that are defined via a browser API. Custom elements are just like those standard HTML elements — names in angle brackets — except they _always_ have a dash in them, like `<news-slider>` or `<bacon-cheeseburger>`. Going forward, browser vendors have committed not to create new built-in elements containing a dash in their names to prevent conflicts.

## HTML templates
```html
<template id="book-template">
<li><span class="title"></span> &mdash; <span class="author"></span></li>
</template> 
<ul id="books"></ul>
```
##### The example above wouldn’t render any content until a script has consumed the template, instantiated the code and told the browser what to do with it.
```javascript
const fragment = document.getElementById('book-template'); 
const books = [ { title: 'The Great Gatsby', author: 'F. Scott Fitzgerald' }, { title: 'A Farewell to Arms', author: 'Ernest Hemingway' }, { title: 'Catch 22', author: 'Joseph Heller' } ]; 
books.forEach(book => { 
// Create an instance of the template content
const instance = document.importNode(fragment.content, true); 
// Add relevant content to the template
instance.querySelector('.title').innerHTML = book.title; instance.querySelector('.author').innerHTML = book.author; 
// Append the instance ot the DOM
document.getElementById('books').appendChild(instance); 
});
```
[[data object + template rendering]]