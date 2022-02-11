```js

function useParam(e) {
	const index = e.target.getAttribute("data-index");
	const parameter = e.target.getAttribute("data-parameter");
	const value = e.target.value;
	if (parameter == "velocity" || parameter == "octave" || parameter == "interval"){
		state.notes[index][parameter] = value;
		pubsub.publish("controls changed", state);
	}
	if (parameter == "transpose") {
		state.transpose = value;
		pubsub.publish("transpose changed", state)
	}
}


function useTheme() {
	const parameter = e.target.getAttribute("data-parameter");
	if (parameter == "theme") {
		state.theme = value;
		pubsub.publish("theme changed")
	}
}




const params = document.querySelectorAll(".param")
[...params.children].forEach(param => {
	note.addEventListener("change", => useParam())
})

const themeToggle = document.querySelector(".toggle");
themeToggle.addEventListener("click", e => useTheme());

//update slider display values on input
const allSliders = document.querySelectorAll("input type=[range]");
[...allSliders].forEach(slider => {
	slider.addEventListener("input",e => updateControlsUI);
})

```

#state #events