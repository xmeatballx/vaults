<iframe width="560" height="315" src="https://www.youtube.com/embed/JrNulEm7GQ0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
	

``` js
const TWO_PI = Math.PI*2.;

let state = {
	transpose: 0,
	notes: [
		{
			interval: 1,
			octave: 4,
			velocity: 1,
			color: [255,0,0],
		},
		{
			interval: 1.15,
			octave: 4,
			velocity: .8,
			color: [137, 215, 220]
		}
	],
	shaderUniforms: {
		wheelRadius: {
			name: "wheelRadius",
			type: "1f",
			value: .9,
		},
		noteRadius: {
			name: "noteRadius",
			type: "1f",
			value: .1,
		},
		noteAngles: {
			name: "angles",
			type: "1fv",
			value: this.notes.map(note => TWO_PI*note.interval+(this.transpose*Math.PI*180)
		},
		noteVelocities: {
			name: "velocities",
			type: "1fv",
			value: this.notes.map(note => note.velocity)
		},
		noteOctaves: {
			name: "octaves",
			type: "1fv",
			value: this.notes.map(note => note.octave/4
		}
		numNotes: {
			name: "numNotes",
			type: "int",
			value: this.notes.length
		}
	},
	theme: light
} 

let styles = {
	note: "note w-full h-max p-3 md:flex md:flex-row",
	controls: "controls w-full",
	interval: "param interval text-base text-mid font-semibold transition ease-in-out m-0 p-1 w-full mb-2 shadow-sm border border-light rounded focus:text-light focus:border-blue-600 focus:outline-none",
	colorPreview: "color_preview w-full h-6",
	octaveContainer: "flex flex-wrap justify-between w-full mt-3",
	octaveLabel: "text-sm text-mid",
	octaveValue: "octave_value text-sm text-mid",
	octave: "param octave slider light mt-3 mb-3 form-range w-full p-0 focus:outline-none focus:ring-0 focus:shadow-none",
	velocityContainer: "flex flex-wrap justify-between w-full",
	velocityLabel: "text-sm text-mid",
	velocityValue: "velocity_value text-sm text-mid",
	velocity: "param velocity slider light mt-3 mb-3 form-range w-full p-0 focus:outline-none focus:ring-0 focus:shadow-none",
	colorPreview2: "color_preview hidden w-2/4 flex-grow ml-3 border-2 border-light"
}

function renderListTemplate(state) {
	const listItems = state.notes.map((note, index) => {
		`<li class=${styles.note} data-index=${index}>
			<div class=${styles.controls}>
				<select name="interval" class=${styles.interval} value=${note.interval}>
					<option value="1" class="text-sm">Fundamental</option>
					<option value="1.067" class="text-sm">Minor Second</option>
					<option value="1.125" class="text-sm">Major Second</option>
					<option value="1.200" class="text-sm">Minor Third</option>
					<option value="1.250" class="text-sm">Major Third</option>
					<option value="1.333" class="text-sm">Perfect Fourth</option>
					<option value="1.414" class="text-sm">Tritone</option>
					<option value="1.500" class="text-sm">Perfect Fifth</option>
					<option value="1.600" class="text-sm">Minor Sixth</option>
					<option value="1.666" class="text-sm">Major Sixth</option>
					<option value="1.777" class="text-sm">Minor Seventh</option>
					<option value="1.875" class="text-sm">Major Seventh</option>
				</select>
				<div class=${styles.colorPreview}></div>
				<div class=${styles.octaveContainer}>
					<label for="octave" class=${styles.octaveLabel}>Octave</label>
					<div class=${styles.octaveValue}>${note.octave}</div>
					<input type="range" name="octave" class=${styles.octave} min="-4" max="4" value=${note.octave}/>
				</div>
				<div class=${styles.velocityContainer}>
						<label for="velocity" class=${styles.velocityLabel}>Velocity</label>
						<div class=${styles.velocityValue}>${note.velocity*100}%</div>
						<input type="range" name="velocity" class="${styles.velocity}" min=0 max=1 value=${note.velocity} step=.1"/>
				</div>
			</div>
			<div class=${styles.colorPreview2}></div>	
		</li>`
	})
	const list = document.querySelector("#notes");
	list.innerHTML = listItems.join('');
}

function updateShaderUniforms() {
	
}



pubsub.subscribe('note added', renderListTemplate)
pubsub.subscribe('note deleted', renderListTemplate)
pubsub.subscribe('controls changed', updateShaderUniforms)
pubsub.subscribe('theme changed', toggleDarkTheme)
```
```javascript
	import pubsub
	import state
	import instrument

	const noteNames = [
		 "C",
		 "C#",
		 "D",
		 "Eb",
		 "E",
		 "F",
		 "F#",
		 "G",
		 "G#",
		 "A",
		 "Bb",
		 "B",
	];

	const pianoOptions = {
	 startOctave: 0,
	 endOctave: 9,
	 keyPressStyle: "vivid",
	}
	const piano = new Instrument(document.getElementById("piano_container"), pianoOptions);
	piano.create();

	function formatNoteName(state, index) {
		const intervalIndex = [...document.querySelectorAll(".interval")][index].selectedIndex;
		return noteNames[intervalIndex].join(state.notes[index].octave);
	}
	
	function updatePiano(state) {
		piano.destroy();
		piano.create();

		state.notes.forEach(note => {
			piano.keyDown(formatNoteName(state, index));
		})
	}

	pubsub.subscribe('controls changed', updatePiano)
	
```
```javascript
	import {Curtains, Plane} from "curtainsjs";

	// wait for everything to be ready
	window.addEventListener("load", () => {
		// set up our WebGL context and append the canvas to our wrapper
		const curtains = new Curtains({
		container: "canvas"
		});
		
		// get our plane element
		const planeElement = document.getElementsByClassName("plane")[0];
		
		// set our initial parameters (basic uniforms)
		const params = {
			vertexShaderID: "plane-vs", // our vertex shader ID
			fragmentShaderID: "plane-fs", // our fragment shader ID
			uniforms: {
				time: {
					name: "uTime", // uniform name that will be passed to our shaders
					type: "1f", // this means our uniform is a float
					value: 0,
				},
			},
		};
		
		// create our plane using our curtains object, the HTML element and the parameters
		const plane = new Plane(curtains, planeElement, params);
		plane.onRender(() => {
			// use the onRender method of our plane fired at each requestAnimationFrame call
			plane.uniforms.time.value++; // update our time uniform value
		});
	});

	function updateShaderUniforms(state) {
		plane.uniforms = state.shaderUniforms;
	}

	pubsub.subscribe('controls changed', updateShaderUniforms)
```
#pubsub #state