# glsl-sh

[![unstable](http://badges.github.io/stability-badges/dist/unstable.svg)](http://github.com/badges/stability-badges)

Get color from spherical harmonic coefficients and normals.

## Installation

`$ npm i -S glsl-sh`

## Usage

In order do use this you need spherical harmonics coefficients. You can generate them with the [cubemap-sh](https://github.com/nicknikolov/cubemap-sh) module which goes hand-in-hand with this module.
A shader to calculate the color would look like this:
```glsl
precision mediump float;
#pragma glslify: sh = require('glsl-sh') // import using glslify
varying vec3 vNormal;
uniform vec3 c[9]; // this is what you get from the cubemap-sh module
uniform vec3 color;
void main() {
  vec3 n = normalize(vNormal);
  vec3 shColor = sh(c, n) * color; // here we get diffuse light calculated by the sperhical harmonics multiplied by the color of the mesh
  gl_FragColor = vec4(shColor, 1.0);
  gl_FragColor.rgb = pow(gl_FragColor.rgb, vec3(1.0 / 2.2)); // gamma correction
}
```
Please note this example uses [glslify](https://github.com/stackgl/glslify).

Please see the cubemap-sh repo for a complete [example](https://github.com/nicknikolov/cubemap-sh/tree/master/example).

## API
`#pragma glslify: sh = require('glsl-sh')`

### sh(vec3[9] c, vec3 normal)
- c: spherical harmonics coefficients
- normal: varying attribute, the normal of the vertex

returns `vec3`, the calculated color

## License
MIT
