.. _variables:

Convsh variables
================

Below is a list of variables which control how convsh does certain functions

**bswap64**
     This boolean value needs to be set to true if 64 bit IEEE UM files have 
     been byte swapped and the files contain 32 bit packed data.
     The default value is false.

**change_mdi**
     Boolean value to control whether the missing data values are changed when
     writing to a file. See **mdival** for the new missing data value. The
     default value is true.

**griblib**
     Selects which library is used to decode GRIB1 data

     | *0*  : ECMWF GRIBEX library (default)
     | *1*  : ECMWF GRIB_API library

**grotype**
     Selects the binary data type for grads output files

     | *0*  : Stream/Direct access (default)
     | *1*  : Sequential (contains Fortran record length headers)

**mdival**
     If **change_mdi** is true set **mdival** to the new missing data value.
     The default value is 2.0e20.

**ncoformat**
     Selects the output netCDF format type, the values are

     | *0*  : classic model (default)
     | *1*  : 64-bit offset
     | *2*  : netCDF-4 classic model

**ncprec**
     Selects the floating point format of netCDF dimensions and
     variables, the values are

     | *32* : 32 bit IEEE (default)
     | *64* : 64 bit IEEE

**red_gauss_conv**
     Selects the method for converting reduced 
     Gaussian GRIB data to full Gaussian GRIB data

     | *0*  : No conversion done
     | *1*  : Linear interpolation (default)
     | *3*  : Cubic interpolation

**umdate**
     Selects how the time dimension for UM ancillary files is created

     | *0*  : Uses PP headers
     | *1*  : Uses Fixed length header (default)

**umlong**
     Selects how the long names of variables from UM/PP files are
     generated, the values are

     | *0*  : Uses PP field code (default)
     | *1*  : Uses STASH code

