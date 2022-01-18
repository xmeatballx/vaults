divide image into numNotes vertical stripes and use js canvas api to get color of each segment
```glsl
	void main()
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    vec3 cols[6] = vec3[6](vec3(1.,0.,0.), vec3(0.,0.,1.), vec3(0.,1.,0.), vec3(.5,.5,0.), vec3(0.,5.,5.), vec3(.5,0.,5.));
    
    
    vec3 col;
    for (float i=0.; i< 6.; i++) {
        float w = 1./6.;
        float rBorder = w + (w)*i;
        float lBorder = rBorder - w;
        if (uv.x < rBorder && uv.x > lBorder) {
            col = cols[int(i)];
        }
    }

    // Output to screen
    fragColor = vec4(col,1.0);
}
	
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