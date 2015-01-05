# df2

Identify clumps within a 3D FITS datacube.

## Quick start guide

To find clumps in your data cube, type

    $ python df2.py my_datacube.fits

To show usage help, type

    $ python df2.py -h

To run in interactive mode, type

     $ python
     >>> import df2
     >>> df2.main(["my_datacube.fits"])

## Description

df2 is an improved implementation of
[DENDROFIND](http://galaxy.asu.cas.cz/~richard/dendrofind/)
([Wunsch et al., 2012](http://adsabs.harvard.edu/abs/2012A%26A...539A.116W))
-- a clump-finding algorithm inspired by
[Clumpfind](http://www.ifa.hawaii.edu/users/jpw/clumpfind.shtml)
([Williams et al., 1994](http://adsabs.harvard.edu/abs/1994ApJ...428..693W)).
DENDROFIND was originally conceived by Richard Wunsch, who also published its
first implementation in Python, later rewritten in C.  Compared to the
original implementation, df2 uses different data structures and doesn't
need parameter `Nlevels`.  df2 is also faster (about 50 000 times) and scales
linearly with the data cube volume (number of pixels).

## Notes

-   Following my tests with real CO data, this program consumes up to 10 times
    the size of the input data cube.  Numpy's `std()` method is especially
    eager for memory and takes about 6 times the size of the array (input data
    cube).  However, if you provide the parameters `--dTleaf` and `--Tcutoff`
    at the command-line, the memory-hungry numpy routines won't be called and
    the memory usage should stay below 5 times the size of your input data
    cube.

-   Tested in Python 2.7 and 3.4.