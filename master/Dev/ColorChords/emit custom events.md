<iframe src="https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events" height=500 style="width: 100%;" id="iframe" loading="lazy"></iframe>


```js

const app = document.querySelector(".root");
const stateChange = new Event('stateChange');

function eventHandler(e) {
	const index = e.target.getAttribute("data-index");
	const parameter = e.target.getAttribute("data-parameter");
	const value = e.target.value;
	state.set(parameter,index,value);
}

app.addEventListener('stateChange', eventHandler(e))

```

#state 