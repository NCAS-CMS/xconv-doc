.. _example3:

Example 3. Extract soil temperature data from ERA monthly mean data
===================================================================

::

 #! /usr/bin/env convsh
 
 #  Convsh script getst.tcl
 #
 #  Extract soil temperature fields from ERA monthly mean, surface GRIB files,
 #  where the ERA data is stored in directory /work/n02/n02/jwc/data on Archer, 
 #  and write out as a netCDF file.
 
 #  Write out netCDF file
 set outformat netcdf
 
 #  Automatically work out input file type
 set filetype 0
 
 #  Convert soil temperature fields only to netCDF
 #  (use Xconv on one file to get soil temperature field numbers)
 set fieldlist "1 6 7 9"
 
 #  Era data is contained in /work/n02/n02/jwc/data directory
 set dir /work/n02/n02/jwc/data
 
 #  Read in each of the ERA monthly mean, surface files and 
 #  write soil temperature fields to the output file
 
 foreach infile [glob $dir/era-20c_surface_N80_*.grib] {
 
 #  Replace input file extension with .nc and append st_ to input 
 #  file name to get output filename
    set outfile "st_[file tail [file rootname $infile].nc]"
 
 #  Read input file
    readfile $filetype $infile
 
 #  Write out soil temperature fields to a netCDF file
    writefile $outformat $outfile $fieldlist
 
 #  Remove input file information from Convsh's memory
    clearall
 }
