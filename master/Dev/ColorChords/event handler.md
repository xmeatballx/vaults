```js

const app = document.querySelector(".root");
const stateChange = new Event('stateChange');

function eventHandler(e) {
	const index = e.target.getAttribute("data-index");
	const parameter = e.target.getAttribute("data-parameter");
	const value = e.target.value;
	if (parameter == "velocity" || parameter == "octave" || parameter == "interval"){
		state.notes[index][parameter] = value;
	}
	if (parameter == "transpose") {
		state.transpose = value;
	}
	if (parameter == )
}

app.addEventListener('stateChange', eventHandler(e))

```

#state #events