.. _example6:

Example 6. Convert fields from grid point GRIB ERA data into UM grid netCDF file
================================================================================

::

 #! /usr/bin/env convsh
 
 #  Convsh script era2um.tcl
 #
 #  Convert ERA grid point surface data into data on the UM climate grid. 
 #  Output format is netCDF. For example:
 #
 #      era2um.tcl -i gpsf90122600 -o gpsf.nc
 
 #  Write out netCDF file
 set outformat netcdf
 
 #  Automatically work out input file type
 set filetype 0
 
 #  Convert PMSL, 2m T fields in input files to netCDF on UM 96x73 grid
 set fieldlist_p "3 6"
 #  Convert 10m u and v fields in input files to netCDF on UM 96x72 grid
 set fieldlist_u "4 5"
 
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
 
 #  Set up 96x73 grid
 set nx 96
 set x0 0.0
 set dx 3.75
 set ny 73
 set y0 90.0
 set dy -2.5
 #  Transform to a regular grid
 setgridtype regular
 #  Define x-axis
 setgrid 1 $nx $x0 $dx
 #  Define y-axis
 setgrid 2 $ny $y0 $dy
 
 #  Interpolate data from 320x160 Gaussian grid to UM 96x73 grid
 interp_grid $fieldlist_p
 
 #  Set up 96x72 grid
 set nx 96
 set x0 1.875
 set dx 3.75
 set ny 72
 set y0 88.75
 set dy -2.5
 #  Transform to a regular grid
 setgridtype regular
 #  Define x-axis
 setgrid 1 $nx $x0 $dx
 #  Define y-axis
 setgrid 2 $ny $y0 $dy
 
 #  Interpolate data from 320x160 Gaussian grid to UM 96x72 grid
 interp_grid $fieldlist_u
 
 #  Write out all input fields to a single netCDF file
 
 writefile $outformat $outfile [concat $fieldlist_p $fieldlist_u]
