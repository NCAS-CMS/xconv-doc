.. _example4:

Example 4. Extract various levels from various fields from ERA monthly mean data
================================================================================

::

 #! /usr/bin/env convsh
 
 #  Convsh script getuvw.tcl
 #
 #  Extract various levels from various fields in ERA monthly mean, 
 #  pressure level GRIB files, where the ERA data is contained in directory 
 #  /work/n02/n02/jwc/data on Archer, and write out as a netCDF file.
 
 #  Write out netCDF file
 set outformat netcdf
 
 #  Automatically work out input file type
 set filetype 0
 
 #  Convert omega, u and v to netCDF 
 #  (use Xconv on one file to get field numbers)
 set fieldlist "2 5 6"
 
 #  Extract omega (2) on pressure levels 300 mb 500 mb and 700 mb.
 #  (use Xconv on one file to get level numbers)
 set levellist1 "8 10 12"
 
 #  Extract u and v (5 and 6) on pressure levels 200 mb 925 mb and 1000 mb.
 set levellist2 "6 15 16"
 
 #  Era data is contained in /work/n02/n02/jwc/data directory
 set dir /work/n02/n02/jwc/data
 
 #  Read in each of the ERA monthly mean, pressure level files and 
 #  write omega, u and v fields to the output file, on specified levels
 
 foreach infile [glob $dir/era-20c_plev_1.125x1.125_*.grib] {
 
 #  Replace input file extension with .nc and append uvw_ to input 
 #  file name to get output filename
    set outfile "uvw_[file tail [file rootname $infile].nc]"
 
 #  Read input file
    readfile $filetype $infile
 
 #  Set the output level dimensions for the output fields
    setdim 3 "2" $levellist1
    setdim 3 "5 6" $levellist2
 
 #  Write out omega, u and v fields to a netCDF file
    writefile $outformat $outfile $fieldlist
 
 #  Remove input file information from Convsh's memory
    clearall
 }
