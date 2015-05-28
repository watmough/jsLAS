# jsLAS

## Experiment to Process Log ASCII Standard Data in a Shader

Yes, text processing in a shader. Right now, I'm write some code to map byte-range flags to 
pretend address offsets in the input texture.

Typically, an input file may be several megs, and the output textures will allow me to find newlines, find depth values and extract depth and columnar data, very quickly.

Output textures are fixed at 256x256 which allows logs up to 65536 entries long. This could be increased.

Input textures will be the size of the input file rounded up to a npot.

There will be the following steps to generate a log:

* scan for newlines (fragment shader -> address of newline)
* scan for depths (fragment shader -> depth values)
* scan for a particular column (fragment shader -> column value)
* generate a blank geometry (javascript/three.js)
* move vertices to represent a digital log (vertex shader)

The last steps will require the geometry shader to read the previous and next log depths and values and spit 
both values onto a line. Note that we'll need to cheat with a vertex attribute to allow the shader to know 
whether to load the first or second position value, as each line will need a top and bottom.

## Status

* I have linear addressing over a texture working correctly with word accuracy when detecting lines,
* Data is passed back in the rendered texture and matches the Javascript code,
