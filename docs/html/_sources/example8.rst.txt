.. _example8:

Example 8. Convert vorticity/divergence spectral data into stream function/velocity potential grid point data
=============================================================================================================

::

 #! /usr/bin/env convsh

 #  Convsh script delm2.tcl
 #
 #  Convert ERA vorticity/divergence spectral data into 
 #  stream function/velocity potential grid point data.
 #  Output format is netCDF. 
 #  For example:
 #
 #      delm2.tcl -i sppr90122600 -o sppr_delm2.nc
  
 #  Write out netCDF file
 set outformat netcdf
 
 #  Automatically work out input file type
 set filetype 0
 
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

 # Select subset of levels
 set levellist "2 7"
 
 # Set output grid type
 setgridtype gaussian
 
 # Set output grid
 setgrid 1 320 0.0 1.125
 setgrid 2 160
 
 # Create Stream function field
 
 set vorid [lsearch -exact [get_shortname -1] VO]
 set sfid [copyfields $vorid]
 set_longname $sfid "Stream function"
 set_shortname $sfid "STRF"
 set_standardname $sfid "atmosphere_horizontal_streamfunction"
 set_unit $sfid "m**2 s**-1"
 
 # Apply del-2 to convert vorticity into stream function
 delm2 $sfid
 
 # Create Velocity potential field
 
 set divid [lsearch -exact [get_shortname -1] D]
 set vpid [copyfields $divid]
 set_longname $vpid "Velocity potential"
 set_shortname $vpid "VPOT"
 set_standardname $vpid "atmosphere_horizontal_velocity_potential"
 set_unit $vpid "m**2 s**-1"
 
 # Apply del-2 to convert divergence into velocity potential
 delm2 $vpid
 
 #  Convert vorid sf div vp fields in input files to netCDF
 set fieldlist [list $vorid $sfid $divid $vpid]
 
 #  Transform data from spectral harmonics to grid point field
 spec_trans $fieldlist
 
 list_fields
 
 #  Set the output level dimensions for the output fields
 setdim 3 $fieldlist $levellist
 
 #  Write out vorid sf div vp input fields to a single netCDF file
 
 writefile $outformat $outfile $fieldlist
