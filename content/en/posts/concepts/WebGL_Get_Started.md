---
Title: "Web GL Get Started"
Description: TODO
tags: ["engine", "webGL"]
draft: true
---

# WebGL

### Basic facts
WebGL runs on the GPU on your computer.
Vertex shader and a fragment shader and they are each written in a very strictly typed C/C++ like language called GLSL (GL Shader Language).
Paired together they are called a program.

### Sending data
There are 4 ways a shader can receive data.
* Attributes and Buffers
* Uniforms : Data are passed to the shader that stay the same for all vertices in a draw call.
* Textures : Data from pixels/texels.
* Varyings : Data passed from the vertex shader and interpolated.

A Vertex shader which provides the clipspace coordinates and a fragment shader that provides the color.
The majority of the WebGL API is about setting up state to supply data to our GLSL programs

### Rendering
In progress

### Keyswords
* attribute
* uniform
* precision medium
* varying

### Notes
* Clipspace coordinates always go from -1 to +1 no matter what size your canvas is
* Colors in WebGL go from 0 to 1.
* You should always set the size you want a canvas with CSS.

### Acknowledgements
Based on the following websites/blog posts :
* [webglfundamentals.org](https://webglfundamentals.org/webgl/lessons/webgl-fundamentals.html)
