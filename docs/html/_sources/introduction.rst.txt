.. _introduction:

Introduction
============

Xconv is a program designed to convert model output into a format suitable 
for use in various plotting packages. Xconv is designed to be simple to use
with a point and click, windows based interface. Xconv can read data in the
following formats: 

* Data output from the Met. Office Unified Model
* Met. Office PP format
* GRIB format (Edition 1 and 2)
* NetCDF format (classic, 64-bit offset and netCDF-4 classic model)
* Grads format

The following output formats are supported by xconv:

* NetCDF format (classic, 64-bit offset and netCDF-4 classic model)
* Grads format

Xconv can be used to see what fields are contained within a data file
and to look at the data values, either directly at the numerical values or
at a grid box fill plot of the data. xconv can also be used to manipulate the 
input data before it is converted into the output format. Data manipulations
available are:

* Spectral data can be transformed to grid point data
* The inverse Laplacian operator can be applied to spectral data
* Grid point data can interpolated onto a different grid using either bilinear interpolation or area weighted interpolation
* Data which is on a rotated grid can be unrotated, plus normal gridded data can be put on a rotated grid.
* Data values can be extrapolated over missing data values
* Zonal and meridonal means can be computed
* The missing data value can be changed

Also available is convsh, which allows scripts to be written to automate 
various xconv tasks. Convsh uses the 
`tcl scripting language <http://www.tcl.tk/man/tcl8.6/TclCmd/contents.htm>`_,
plus various extensions for reading, writing and manipulating data files.
