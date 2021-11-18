# FACET-II-Flattening
Model for flat beam generation at FACET-II linear accelerator. Contains a GPT input deck to perform calculations via simulation, as well as python notebooks for post processing and
optimization of simulation results. 

# Usage
The GPT model of the beamline from photogun to L0BF exit must be run via run_facet.bat to produce an accelerated beam. User has the option to let GPT generate the beam according to input specifications, read in a beam from an external gdf, or load in a beam from a bitmap. This beam is used as the input for a second simulation through the ~5 meters following the injector exit, where skew-quadrupole lattice may be placed. The beam data may be dumped at any location after it's initial post-acceleration drift. 

The distances from the dump location to the (centroid of) the first quad, from first to second quad, and from second to third quad (d0, d1, d2, respectively) are chosen "manually" by the user, and a check must be performed to ensure that the quad positions do not overlap with existing quads that have fixed positions. These parameters are then used to produce an analytical estimate for the skew-quadrupole strengths via the init_guess function. A Nelder-Mead optimization using the analytic estimate as an objective function may be performed, after which another Nelder-Mead optimization, using the output of the GPT simulation with full 3D space-charge, is performed to minimize the emittance ratio εy/εx.
