.. _example9:

Example 9. Convert multiple files into single 64-bit netCDF4 file using CF metadata
===================================================================================

::

 #! /usr/bin/env convsh

 #  Convsh script conv2nc_cf.tcl
 #
 #  Convert input files into single netCDF4 file with CF metadata.
 #  All input files must contain the same fields and have
 #  identical dimensions except for the time dimension.
 #  For example to convert UM output files into a netCDF file
 #  use the following command:
 #
 #      conv2nc_cf.tcl -i xaavaa.pc* -o xaava.nc
 
 #  Use CF compatible netCDF attributes + useful others
 setvaratt all att_nouse
 setvaratt north_pole standard_name att_cond
 setvaratt long_name units missing_value _Fillvalue valid_min valid_max att_use
 setdimatt all att_nouse
 setdimatt standard_name calendar att_cond
 setdimatt long_name units axis time_origin positive att_use
 
 #  Set netCDF global attribute Conventions
 setglobatt Conventions att_use
 writeglobatt Conventions "CF-1.5"
 
 #  Use STASH code to get UM variable long names
 set umlong 1
 
 #  Write out netCDF file
 set outformat netcdf
 #  Set netCDF format to be netCDF4 classic model
 set ncoformat 2
 # Set netCDF precision to 64 bit
 set ncprec 64
 
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
          if {$i} {example9.rst
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
 
 #  Write out all input fields to a single netCDF file
 
 writefile $outformat $outfile $fieldlist
