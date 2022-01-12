divide image into numNotes vertical stripes and use js canvas api to get color of each segment
```glsl
	void main() {
		vec4 image = texture(iChannel0, uv);
    
	    vec4 col;
	    float angles[] = float[6](0.,1.,2.,3.,4.,5.);
	    float offsets[6] = float[6](1.,1.,1.,1.,1.,1.);
	    float octaves[6] = float[6](0.,0.,-.2,.5,-1.,1.);
	    
	    for (int i=0;i<12;i++){
	        if (i<6) {
		        vec2 offset = vec2(sin(angles[i]),cos(angles[i]));
		        vec2 pos = uv + (offset*offsets[i])*.4;
		        c = texture(iChannel0,offset)+vec4(vec3(octaves[i]),1.);
				///check if uv within segment width + stripeOffset and add c to col
			}
		}
		gl_FragColor = 
	
```

```js
	const canvas = document.querySelector("#canvas")
	const c = canvas.getGontext('2d');
	const colors = [];
	for (i=0;i<state.notes.length;i++) {
		const x = canvas.width/state.notes.length*i+1;
		c.getImageData(x,1,1,1)
	}
```