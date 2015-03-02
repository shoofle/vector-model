# vector-model
just a lil' scratch pad for a vector graphics model / language / thing / idk.

## models
shader:
- it's a shader. defines how to draw a region.
- not, at the moment, up for particular customization; somewhat beyond the reach of this thought experiment

group:
- groups a bunch of elements to be referred to by the same thing
- has an associated transform to be applied before evaluating positions of children

region:
- closed region in the drawing world.
- has an associated or implied path around it.
- must be connected? or not? idk.

path:
- defines a connected sequence of lines or curves, one after another
- typically defined in terms of path nodes, as in the svg path style or the spline style

[svg-style path nodes](http://www.w3.org/TR/SVG/paths.html#PathDataMovetoCommands):
- each node consists of a one-character instruction followed by several numerical parameters
- they indicate what kind of shape to draw and how far and such, for example:
  - `M10 15`: *M*ove (without drawing a line) to the absolute coordinate `10, 15` 
  - `c10 13 16 20 30 30`: *c*ubic bezier spline ending at `30, 30`, with control points at `10, 13` and `16, 20` (all relative to the path's starting point)
- in SVG, the path data is set as a string on the path element. that sucks and i hate it. esp. given how much paths get used.

spline-style path nodes:
- each node (in a bezier curve) has an incoming control handle and an outgoing control handle
- presumably given that we've got two handles between each node, it's always cubic, but segments can be modified to increase the number of segments maybe?
- you additionally have toggles to change the behavior of a node, between such things as:
  - handles locked to antiparallel and same length
  - handles antiparallel but variable length
  - handles free (so this node will be a corner)
  - path ends or starts at this node (no path drawn between this and the next/previous nodes)

I guess you can pretty easily transform from one of those to the other, but I'd like easy access to any node in terms of either one - it'd be a huge pain to make a spline editor if you can only work in terms of svg pathdata. i want access to the handles.
