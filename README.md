# pbrt-v4-menger

![menger img](/img/menger.png)

This is an example of creating a [Menger Sponge](https://en.wikipedia.org/wiki/Menger_sponge) in pbrt-v4 by abusing the Import/Include directives.

The scene contains a Menger Sponge of 10 iterations, 10,240,000,000,000 boxes, and is constructed using a combination of ObjectInstances and nested Includes. To get to the 10 iterations we use-
* 4 iterations - PlyMesh geometry that is ~1,920,000 triangles.
* 1 iteration - Placing the PlyMesh 20 times
* 5 iterations - Utilizing the iterative nature of the Menger Sponge we can repeatedly apply the same set of transforms, nesting Includes as we go.

This gives us our 10 iterations and will require roughly 3GB to 4GB of VRAM to render on the GPU.

If you happen to have over 15GB GB of VRAM on your GPU you can edit the `scene.pbrt` and use 
```
Include "./instancing/instancer_6.pbrt"
```
This will give you 11 iterations, or 204,800,000,000,000 boxes.

### Notes
When using the `instancer_6.pbrt`, it uses `Imports` instead of `Includes` which allows the nested structures to be built across 20 different threads greatly speeding up the load time. On my machine when rendering `instancer_6.pbrt` the time to first pixel is about 50s.

Try it out in interactive mode!
`pbrt --interactive --gpu scene.pbrt`

