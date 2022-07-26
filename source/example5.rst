.. _example5:

Example 5. Convert spectral GRIB ERA data into single grid point netCDF file
============================================================================

::

 #! /usr/bin/env convsh
 
 #  Convsh script era2grid.tcl
 #
 #  Convert ERA spectral data into grid point data. Output format is netCDF. 
 #  For example:
 #
 #      era2grid.tcl -i sppr90122600 -o sppr.nc
 
 #  Write out netCDF file
 set outformat netcdf
 
 #  Automatically work out input file type
 set filetype 0
 
 #  Convert all fields in input files to netCDF
 set fieldlist -1
 
 #  Get command line arguments:
 #      -i input files (can be more than one file)
 #      -o output file (single file only)
 
 set i false
 set o false
 foreach arg $argv {
    switch -glob -- $arg {
       -i      {set i true ; set o false}
       -o      {set i false ; set o true}
       -*      {puts "unknown option $arg" ; set i false; set o false}
       default {
          if {$i} {
             set infile [lappend infile $arg]
          } elseif {$o} {
             set outfile [lappend outfile $arg]
          } else {
             puts "unknown option $arg"
          }
       }
    }
 }
 
 if {! [info exists infile]} {
    puts "input file name must be given"
    exit
 }
 
 if {[info exists outfile]} {
    if {[llength $outfile] > 1} {
       set outfile [lindex $outfile 0]
       puts "Only one output file can be specified, using $outfile"
    }
 } else {
    puts "output file name must be given"
    exit
 }
 
 #  Read in each of the input files
 
 foreach file $infile {
    readfile $filetype $file
 }
 
 #  Transform data from spectral harmonics to the equivalent grid point field
 #  (T106 data -> 320x160 Gaussian grid)
 
 spec_trans $fieldlist
 
 #  Write out all input fields to a single netCDF file
 
 writefile $outformat $outfile $fieldlist
