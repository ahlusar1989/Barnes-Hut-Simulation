# Barnes-Hut-Simulation

Implementation of a the parallel Barnes-Hut algorithm for N-body simulation. 
N-body simulation is a simulation of a system of N particles that interact 
with physical forces, such as gravity or electrostatic force. Given initial 
positions and velocities of all the particles (or bodies), the N-body simulation
computes the new positions and velocities of the particles as the time progresses. 
It does so by dividing time into discrete short intervals, and computing the 
positions of the particles after each interval.


To take advantage of this observation, the Barnes-Hut algorithm relies on a quadtree -- 
a data structure that divides the space into cells, and answers queries such as 'What is 
the total mass and the center of mass of all the particles in this cell?'.


An iteration of the Barnes-Hut algorithm is composed of the following steps:

1. Construct the quadtree for the current arrangement of the bodies.
2. Determine the boundaries, i.e. the square into which all bodies fit.
3. Construct a quadtree that covers the boundaries and contains all the bodies.

4. Update the bodies -- for each body:
⋅⋅1. Update the body position according to its current velocity.
⋅⋅2. Using the quadtree, compute the net force on the body by adding the individual forces from all the other bodies.
⋅⋅3. Update the velocity according to the net force on that body.


It turns out that, for most spatial distribution of bodies, the expected number of cells that contribute to the net force on a body is log n, so the overall complexity of the Barnes-Hut algorithm is O(n log n).

The main source directory contains an implementation of the following:

a quadtree and its combiner data structure
an operation that computes the total force on a body using the quadtree
a simulation step of the Barnes-Hut algorithm
