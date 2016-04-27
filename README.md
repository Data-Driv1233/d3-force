# d3-force

…

## Installing

If you use NPM, `npm install d3-force`. Otherwise, download the [latest release](https://github.com/d3/d3-force/releases/latest). You can also load directly from [d3js.org](https://d3js.org), either as a [standalone library](https://d3js.org/d3-force.v0.2.min.js) or as part of [D3 4.0 alpha](https://github.com/mbostock/d3/tree/4). AMD, CommonJS, and vanilla environments are supported. In vanilla, a `d3_force` global is exported:

```html
<script src="https://d3js.org/d3-collection.v0.1.min.js"></script>
<script src="https://d3js.org/d3-dispatch.v0.4.min.js"></script>
<script src="https://d3js.org/d3-quadtree.v0.7.min.js"></script>
<script src="https://d3js.org/d3-timer.v0.4.min.js"></script>
<script src="https://d3js.org/d3-force.v0.2.min.js"></script>
<script>

var simulation = d3_force.forceSimulation(nodes);

</script>
```

[Try d3-force in your browser.](https://tonicdev.com/npm/d3-force)

## API Reference

…

### Simulation

…

<a name="forceSimulation" href="#forceSimulation">#</a> d3.<b>forceSimulation</b>([<i>nodes</i>])

…

<a name="simulation_start" href="#simulation_start">#</a> <i>simulation</i>.<b>start</b>()

…

<a name="simulation_stop" href="#simulation_stop">#</a> <i>simulation</i>.<b>stop</b>()

…

<a name="simulation_tick" href="#simulation_tick">#</a> <i>simulation</i>.<b>tick</b>()

…

<a name="simulation_nodes" href="#simulation_nodes">#</a> <i>simulation</i>.<b>nodes</b>([<i>nodes</i>])

…

* `index` - the node’s zero-based index into *nodes*
* `x` - the node’s current *x*-position
* `y` - the node’s current *y*-position
* `vx` - the node’s current *x*-velocity
* `vy` - the node’s current *y*-velocity

<a name="simulation_alphaMin" href="#simulation_alphaMin">#</a> <i>simulation</i>.<b>alphaMin</b>([<i>alpha</i>])

…

<a name="simulation_alphaDecay" href="#simulation_alphaDecay">#</a> <i>simulation</i>.<b>alphaDecay</b>([<i>decay</i>])

…

<a name="simulation_drag" href="#simulation_drag">#</a> <i>simulation</i>.<b>drag</b>([<i>drag</i>])

…

<a name="simulation_force" href="#simulation_force">#</a> <i>simulation</i>.<b>force</b>(<i>name</i>[, <i>force</i>])

…

<a name="simulation_on" href="#simulation_on">#</a> <i>simulation</i>.<b>on</b>(<i>typenames</i>, [<i>callback</i>])

…

### Forces

[Simulations](#simulation) compose multiple arbitrary forces. By default, simulations have no bound forces; add or remove a force using [*simulation*.force](#simulation_force). This module provides several built-in forces:

* [Centering](#centering)
* [Circle Collision](#circle-collision)
* [Circle Containment](#circle-containment)
* [Links](#links)
* [Many-Body](#many-body)
* [Positioning](#positioning)

You may also implement your own custom force. A force is simply a [function](#_force) that takes the simulation’s current *alpha* value and then modifies nodes’ positions or velocities. Forces may optionally implement [*force*.initialize](#force_initialize) to receive the simulation’s array of nodes.

<a name="_force" href="#_force">#</a> <i>force</i>(<i>alpha</i>)

…

<a name="force_initialize" href="#force_initialize">#</a> <i>force</i>.<b>initialize</b>(<i>nodes</i>)

…

#### Centering

The centering force moves nodes so that their center of mass (assuming all nodes are equal-weight) is at the given position ⟨[*x*](#center_x),[*y*](#center_y)⟩. (These parameters are only recomputed when the force is initialized, not on every application.)

<a name="forceCenter" href="#forceCenter">#</a> d3.<b>forceCenter</b>([<i>x</i>, <i>y</i>])

…

<a name="center_x" href="#center_x">#</a> <i>center</i>.<b>x</b>([<i>x</i>])

…

<a name="center_y" href="#center_y">#</a> <i>center</i>.<b>y</b>([<i>y</i>])

…

#### Circle Collision

The circle collision force prevents circular nodes with a given [radius](#collide_radius) from overlapping. More formally, two nodes *a* and *b* are separated so that the distance between *a* and *b* is at least *radius*(*a*) + *radius*(*b*). To reduce jitter, this is by default a “soft” constraint with a configurable [strength](#collide_strength). (These parameters are only recomputed when the force is initialized, not on every application.)

<a name="forceCollide" href="#forceCollide">#</a> d3.<b>forceCollide</b>([<i>radius</i>])

…

<a name="collide_radius" href="#collide_radius">#</a> <i>collide</i>.<b>radius</b>([<i>radius</i>])

…

<a name="collide_strength" href="#collide_strength">#</a> <i>collide</i>.<b>strength</b>([<i>strength</i>])

…

#### Circle Containment

The circle containment force constrains nodes to fit within a circle of a given [*radius*](#contain_radius) and center ⟨[*x*](#contain_x),[*y*](#contain_y)⟩. The radius and center can be specified on a per-node basis. (These parameters are only recomputed when the force is initialized, not on every application.)

<a name="forceContain" href="#forceContain">#</a> d3.<b>forceContain</b>([<i>radius</i>[, <i>x</i>, <i>y</i>]])

…

<a name="contain_radius" href="#contain_radius">#</a> <i>contain</i>.<b>radius</b>([<i>radius</i>])

…

<a name="contain_x" href="#contain_x">#</a> <i>contain</i>.<b>x</b>([<i>x</i>])

…

<a name="contain_y" href="#contain_y">#</a> <i>contain</i>.<b>y</b>([<i>y</i>])

…

#### Links

The link force pushes linked nodes closer together or farther apart according to the desired [link distance](#link_distance), which may be specified on a per-node basis. (These parameters are only recomputed when the force is initialized, not on every application.)

<a name="forceLink" href="#forceLink">#</a> d3.<b>forceLink</b>([<i>links</i>])

If *links* is specified, sets the layout's associated links to the specified array. If *links* is not specified, returns the current array, which defaults to the empty array. Each link has the following attributes:

* source - the source node (an element in *nodes*).
* target - the target node (an element in *nodes*).

Note: the values of the source and target attributes may be initially specified as indexes into the *nodes* array; these will be replaced by references after the call to [start](#start). Link objects may have additional fields that you specify; this data can be used to compute link [strength](Force-Layout#linkStrength) and [distance](Force-Layout#linkDistance) on a per-link basis using an accessor function.

<a name="link_links" href="#link_links">#</a> <i>link</i>.<b>links</b>([<i>links</i>])

…

* `index` - the zero-based index into *links*
* `source` - the link’s source node; see [*simulation*.nodes](#simulation_nodes)
* `target` - the link’s target node; see [*simulation*.nodes](#simulation_nodes)

The source and target properties may be initialized using [*link*.id](#link_id).

<a name="link_id" href="#link_id">#</a> <i>link</i>.<b>id</b>([<i>id</i>])

If *id* is specified, sets the string identifier of linking to the specified value.

<a name="link_strength" href="#link_strength">#</a> <i>link</i>.<b>strength</b>([<i>strength</i>])

If *strength* is specified, sets the strength (rigidity) of links to the specified value in the range [0,1]. If *strength* is not specified, returns the layout's current link strength, which defaults to 1. If *strength* is a constant, then all links have the same strength. Otherwise, if *strength* is a function, then the function is evaluated for each link (in order), being passed the link and its index, with the `this` context as the force layout; the function's return value is then used to set each link's strength. The function is evaluated whenever the layout [starts](Force-Layout#start).

<a name="link_distance" href="#link_distance">#</a> <i>link</i>.<b>distance</b>([<i>distance</i>])

If *distance* is specified, sets the target distance between linked nodes to the specified value. If *distance* is not specified, returns the layout's current link distance, which defaults to 20. If *distance* is a constant, then all links are the same distance. Otherwise, if *distance* is a function, then the function is evaluated for each link (in order), being passed the link and its index, with the `this` context as the force layout; the function's return value is then used to set each link's distance. The function is evaluated whenever the layout [starts](Force-Layout#start).

Links are not implemented as "spring forces", as is common in other force-directed layouts, but as weak geometric constraints. For each tick of the layout, the distance between each pair of linked nodes is computed and compared to the target distance; the links are then moved towards each other, or away from each other, so as to converge on the desired distance. This method of constraints relaxation on top of position Verlet integration is vastly more stable than previous methods using spring forces, and also allows for the flexible implementation of [other constraints](http://www.csse.monash.edu.au/~tdwyer/Dwyer2009FastConstraints.pdf) in the tick event listener, such as hierarchical layering.


#### Many-Body

The many-body (or *n*-body) force applies mutally amongst all [nodes](#simulation_nodes). It can be used to simulate gravity (attraction) if the [strength](#manyBody_strength) is positive, or eletrical charge (repulsion) if the strength is negative. This implementation uses quadtrees and the [Barnes–Hut approximation](https://en.wikipedia.org/wiki/Barnes–Hut_simulation) to greatly improve performance; the accuracy can be customized using the [theta](#manyBody_theta) parameter. The strength can be specified on a per-node basis. (This parameter is only recomputed when the force is initialized, not on every application.)

<a name="forceManyBody" href="#forceManyBody">#</a> d3.<b>forceManyBody</b>()

…

<a name="manyBody_strength" href="#manyBody_strength">#</a> <i>manyBody</i>.<b>strength</b>([<i>strength</i>])

…

<a name="manyBody_theta" href="#manyBody_theta">#</a> <i>manyBody</i>.<b>theta</b>([<i>theta</i>])

…

<a name="manyBody_distanceMin" href="#manyBody_distanceMin">#</a> <i>manyBody</i>.<b>distanceMin</b>([<i>distance</i>])

…

<a name="manyBody_distanceMax" href="#manyBody_distanceMax">#</a> <i>manyBody</i>.<b>distanceMax</b>([<i>distance</i>])

…

#### Positioning

The positioning force pushes nodes towards a desired position ⟨[*x*](#position_x),[*y*](#position_y)⟩. The position and [strength](#position_strength) can be specified on a per-node basis. (These parameters are only recomputed when the force is initialized, not on every application.)

<a name="forcePosition" href="#forcePosition">#</a> d3.<b>forcePosition</b>([<i>x</i>, <i>y</i>])

…

<a name="position_strength" href="#position_strength">#</a> <i>position</i>.<b>strength</b>([<i>strength</i>])

…

<a name="position_x" href="#position_x">#</a> <i>position</i>.<b>x</b>([<i>x</i>])

…

<a name="position_y" href="#position_y">#</a> <i>position</i>.<b>y</b>([<i>y</i>])

…
