# jsLAS

Experiment to Process Log ASCII Standard Data in a Shader

Yes, text processing in a shader. Right now, I'm write some code to map byte-range flags to pretend address offsets 
in the input texture.

Typically, an input file may be several megs, and the output textures will allow me to find newlines, find depth values and extract depth and columnar data.

There will be the following steps to generate a log:

* scan for newlines (fragment shader)
* scan for depths (fragment shader)
* scan for a particular column (fragment shader)
* generate a blank geometry (javascript/three.js)
* move vertices to represent a digital log (vertex shader)

The last steps will require the geometry shader to read the previous and next log depths and values and spit 
both values onto a line. Note that we'll need to cheat with a vertex attribute to allow the shader to know 
whether to load the first or second position value, as each line will need a top and bottom.
