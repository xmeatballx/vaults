## Push dist folder to gh-pages branch
```
git subtree push --prefix dist origin gh-pages
```

---

## RGBtoHSV
```javascript
/* accepts parameters
 * r  Object = {r:x, g:y, b:z}
 * OR 
 * r, g, b
*/
function RGBtoHSV(r, g, b) {
    if (arguments.length === 1) {
        g = r.g, b = r.b, r = r.r;
    }
    var max = Math.max(r, g, b), min = Math.min(r, g, b),
        d = max - min,
        h,
        s = (max === 0 ? 0 : d / max),
        v = max / 255;

    switch (max) {
        case min: h = 0; break;
        case r: h = (g - b) + d * (g < b ? 6: 0); h /= 6 * d; break;
        case g: h = (b - r) + d * 2; h /= 6 * d; break;
        case b: h = (r - g) + d * 4; h /= 6 * d; break;
    }

    return {
        h: h,
        s: s,
        v: v
    };
}
```

---

## RGBtoHex
```javascript
function componentToHex(c) {
  var hex = c.toString(16);
  return hex.length == 1 ? "0" + hex : hex;
}

function rgbToHex(r, g, b) {
  return "#" + componentToHex(r) + componentToHex(g) + componentToHex(b);
}
```

---

## Add border to sdf
```glsl
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
```

---

## SDF circle
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


```