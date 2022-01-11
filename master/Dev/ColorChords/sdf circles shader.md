```glsl
float circleSDF(
    float x,
    float y,
    float cx,
    float cy, 
    float r)
{
    // Sample coordinates relative to circle center.
    float _x = x - cx;
    float _y = y - cy;
    
    // Signed distance.
    return sqrt(_x * _x + _y *_y) - r;
}

vec4 addBorder(float d, float width, vec4 border, vec4 fill, vec4 background) {
    if (d < -width) {
        return fill;
    }
    if (d < 0.) {
        float t = -d / width;
        t = t * t;
        return mix(border,fill,t);
    }
    if (d < width) {
        float t = d / width;
        t = t * t;
        return mix(border,background,t);
    }
}

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    
    vec4 bc = vec4(0.,0.,0.,1.);
    vec4 c = vec4(1.,0.,0.,1.);
    vec4 bg = vec4(1.);
    float borderThickness = .004;


    // Time varying pixel color
    vec4 image = texture(iChannel0, uv);
    
    vec4 col;
    float angles[6] = float[6](0.,1.,2.,3.,4.,5.);
    float offsets[6] = float[6](1.,1.,1.,1.,1.,1.);
    float octaves[6] = float[6](0.,0.,-.2,.5,-1.,1.);
    
    for (int i=0;i<12;i++){
        if (i<6) {
        vec2 offset = vec2(sin(angles[i]),cos(angles[i]));
        vec2 pos = uv + (offset*offsets[i])*.4;
        float sdf = circleSDF(.5,.5,pos.x,pos.y,.05);
        c = texture(iChannel0,offset)+vec4(vec3(octaves[i]),1.);
        
        col += (sdf > borderThickness) ? vec4(0.) : addBorder(sdf,borderThickness,bc,c,image);
        }
    }

    // Output to screen
    fragColor =  col.z == 0. ? image : col;
}

```

#shader #sdf #circle