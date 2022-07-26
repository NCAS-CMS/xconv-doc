.. _cmd_line_args:

Command line arguments 
======================

Xconv can be given the following command line arguments: ::

   -i input file names : specify a number of files to be read into xconv, wildcard characters can be used
   -o output file name : specify a single output file name

For example if you wished to read UM files which have file names beginning 
with xafma.pa, and you wanted to write the output to a netCDF file called
ppa.nc, then use the following xconv command: ::

   xconv -i xafma.pa* -o ppa.nc
