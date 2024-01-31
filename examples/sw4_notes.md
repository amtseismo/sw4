# SW4 Notes

## Running stuff
`mpirun -host localhost -np 2 ../../optimize/sw4 seismic1.in`

## Lambs problem from CIG/LLNL tutorial
This file sets up Lambs problem with a point source aligned with the z - axis  

This line gives the output file name. 

`fileio path=seis-out`

This line sets up the grid with the number of #x elements= #y elements = #z elements = 200.  x grid size is 30 km, y grid size is 30 km and z grid size is 10 km in depth.  Az=0 sets x=North, y=East, and Z=down.

`grid h=200 x=30e3 y=30e3 z=10e3 az=0`

Set simulation time
`time t=15.0`

Sets velocity model to be vs=1000 m/s, vp=sqrt(3)*1000 m/s, and rho=1500 kg/m^3

`block vp=1.7320508076e+03 vs=1000 rho=1500`

For sources need to prescribe the type=C6SmoothBump, location (x=15e3 y=15e3 z=0), magnitude (10^13 N), frequency (0.42 Hz), and t0 (starting time)

`source type=C6SmoothBump x=15e3 y=15e3 z=0 fz=1e13 freq=0.42 t0=0`

Important: To avoid artifacts from a sudden startup, use t0 ≥ 1.35/ω.  So why does above example have t0=0?

Time history of solution along a vertical line aligned with the source.  This puts sensor at x, y, z coordinates, specifies output file names, specifies nsew ground motions, and usgsformat (output all components in an ASCII text file).

`rec x=15e3 y=16e3 z=0 file=v1 nsew=1 usgsformat=1`
`rec x=15e3 y=25e3 z=0 file=v10 nsew=1 usgsformat=1`