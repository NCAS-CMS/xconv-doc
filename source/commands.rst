.. _commands:

Convsh commands
===============

Below is a list of convsh extensions to the 
`tcl scripting language <http://www.tcl.tk/man/tcl8.6/TclCmd/contents.htm>`_. 
Some commands have the argument *fieldlist*, this is a list of numbers which
represents a subset of the fields which convsh has stored in memory. These
fields will be stored in the same order as they are in xconv, 
therefore the easiest way to
work out the field numbers is to run xconv on one file, before applying a
convsh script to a large number of files. Remember field numbering starts at 0.
A field number of -1 is  shorthand for specifying all field numbers convsh
currently has stored in memory.

**clearall**
     Clears away all internal information about previous input files. This
     command must be used if a separate output file is needed for every 
     input file.

**copyfields** *fieldlist*
     Make a copy of all the fields in *fieldlist*. These additional fields
     will be appended to the list of fields convsh has stored in memory. The 
     command will return the field numbers of the newly created fields.
     For example if the original fields are (a,b,c,d,e) mapped on to field 
     numbers (0,1,2,3,4), after the command **copyfields** *"1 3"*, the new 
     fields will be (a,b,c,d,e,b,d) mapped on to field numbers (0,1,2,3,4,5,6). 
     The command will return "5 6".

**delfields** *fieldlist*
     Delete all the fields in *fieldlist*. Note the field numbers
     will be changed by this command. For example if the original fields are
     (a,b,c,d,e) mapped on to field numbers (0,1,2,3,4), after the command
     **delfields** *"1 3"*, the new fields will be (a,c,e) mapped on
     to field numbers (0,1,2). 

**delm2** *fieldlist*
     Compute the inverse Laplacian of the spectral harmonic coefficients in 
     *fieldlist*

**edit_grid** *fieldlist*
     For each of the fields in *fieldlist* change the values of the x and y 
     dimensions but not the number of rows or columns. The new x,y dimensions
     values are set by running either the **setgrid** or **settrunc** command.

**extendglobatt** *attribute value*
     Extend global attribute *attribute* with *value*.

**extrap** *fieldlist minnbr*
     For each of the fields in *fieldlist* extrapolate over missing data using
     nearest neighbour filling. The value of *minnbr* selects the minimum 
     number of nearest neighbours used and should be a value between 1 and 4.

**get_cal** *fieldlist*
     For each of the fields in *fieldlist* get the calendar type. The command
     return a list of integers where the integer value represents a calendar 
     type

     | *1*  : Gregorian calendar
     | *2*  : 360 day calendar
     | *14* : Julian calendar
     | *15* : No leap year calendar

**get_description** *fieldlist*
     For each of the fields in *fieldlist* get the description string. For 
     netCDF files the description string will be taken from the *source*
     attribute, if that doesn't exist then it will be taken from the *comments*
     attribute.

**get_gridtype** *fieldlist*
     For each of the fields in *fieldlist* get the grid type. The command
     return a list of integers where the integer value represents a grid type

     | *0*  : Gaussian latitude/longitude grid
     | *1*  : Regular latitude/longitude grid
     | *2*  : Reduced Gaussian latitude/longitude grid
     | *3*  : Spectral harmonic coefficients
     | *4*  : Polar stereographic grid
     | *5*  : Space view perspective or orthographic grid
     | *6*  : Mercator projection grid
     | *7*  : Gnomonic projection grid
     | *8*  : Plane polar grid
     | *9*  : Plane Cartesian grid
     | *10* : Staggered latitude/longitude grid
     | *11* : Reduced regular latitude/longitude grid

**get_longname** *fieldlist*
     For each of the fields in *fieldlist* get the long name string. For 
     netCDF files the long name string will be taken from the *long_name*
     attribute, if that doesn't exist then it will be taken from the *title*
     attribute, if that doesn't exist then it will be taken from the 
     *standard_name* attribute.

**get_mdi** *fieldlist*
     For each of the fields in *fieldlist* get the missing data indicator value.

**get_shortname** *fieldlist*
     For each of the fields in *fieldlist* get the short name string. For 
     netCDF files the short name string will be taken from the variable name.

**get_standardname** *fieldlist*
     For each of the fields in *fieldlist* get the standard name string. For 
     netCDF files the standard name string will be taken from the 
     *standard_name* attribute.

**get_tlongname** *fieldlist*
     For each of the fields in *fieldlist* get the time dimension long name string. 

**get_tname** *fieldlist*
     For each of the fields in *fieldlist* get the time dimension name string. 

**get_tstandardname** *fieldlist*
     For each of the fields in *fieldlist* get the time dimension standard name string. 

**get_tunit** *fieldlist*
     For each of the fields in *fieldlist* get the time dimension unit string. 

**get_unit** *fieldlist*
     For each of the fields in *fieldlist* get the unit string. For 
     netCDF files the unit string will be taken from the 
     *units* attribute.

**get_xlongname** *fieldlist*
     For each of the fields in *fieldlist* get the x dimension long name string.

**get_xname** *fieldlist*
     For each of the fields in *fieldlist* get the x dimension name string. 

**get_xstandardname** *fieldlist*
     For each of the fields in *fieldlist* get the x dimension standard name string. 

**get_xunit** *fieldlist*
     For each of the fields in *fieldlist* get the x dimension unit string. 

**get_ylongname** *fieldlist*
     For each of the fields in *fieldlist* get the y dimension long name string. 
**get_yname** *fieldlist*
     For each of the fields in *fieldlist* get the y dimension name string. 

**get_ystandardname** *fieldlist*
     For each of the fields in *fieldlist* get the y dimension standard name string. 

**get_yunit** *fieldlist*
     For each of the fields in *fieldlist* get the y dimension unit string. 

**get_zlongname** *fieldlist*
     For each of the fields in *fieldlist* get the z dimension long name string.

**get_zname** *fieldlist*
     For each of the fields in *fieldlist* get the z dimension name string. 

**get_zstandardname** *fieldlist*
     For each of the fields in *fieldlist* get the z dimension standard name string. 

**get_zunit** *fieldlist*
     For each of the fields in *fieldlist* get the z dimension unit string. 

**getdimatt** *attribute1 attribute2 attribute3 ...*
     The command returns a list where each element is the dimension attribute 
     state for the corresponding attribute argument. The dimension attribute 
     state can have one of the following values

     | *att_use*   : This attribute will be used for all relevant dimensions
     | *att_nouse* : This attribute will not be used for any dimensions
     | *att_cond*  : This attribute will be used only when there is data 
                     available or when the attribute value is different 
                     from the assumed default value.

**getglobatt** *attribute1 attribute2 attribute3 ...*
     The command returns a list where each element is the global attribute 
     state for the corresponding attribute argument. The global attribute 
     state can have one of the following values

     | *att_use*   : This global attribute will be used
     | *att_nouse* : This global attribute will not be used

**getvaratt** *attribute1 attribute2 attribute3 ...*
     The command returns a list where each element is the variable attribute 
     state for the corresponding attribute argument. The variable attribute 
     state can have one of the following values

     | *att_use*   : This attribute will be used for all variables
     | *att_nouse* : This attribute will not be used for any variables
     | *att_cond*  : This attribute will be used only when there is data 
                     available or when the attribute value is different 
                     from the assumed default value.

**interp_grid** *fieldlist*
     Interpolate data, for fields in *fieldlist*, from one grid to 
     another. The initial grid will either 
     be the grid the data was read in on, or the grid from a previous 
     **interp_grid** or **spec_trans** command. If a new grid is not
     defined using **setgrid** or **settrunc**, the new grid will be the 
     same as the initial grid. 

**list_fields** [*fieldtitle*]
     List all of the fields currently active in convsh. The output format is
     the same as in the main xconv window. The *fieldtitle* argument is
     optional, it can have three values *short*, *long* and 
     *both*. *short* uses the
     short form of the field title, *long* uses the long form and 
     *both* uses both.
     If *fieldtitle* is not given the long form of the field title is 
     used. 

**meridonal_mean** *fieldlist*
     For each of the fields in *fieldlist* calculate the meridonal mean.

**readfile** *filetype filename*
     Read into convsh the file given by *filename*, the file type is
     given by the *filetype* argument. If *filetype* has the value
     *0* convsh will try to automatically determine the file type, this 
     will usually work but if it fails the actual file type can be given. 
     The various values of *filetype* for different input file types 
     are given below:
     
     | *0*   : Automatic
     | *1*   : UM format (32 bit IEEE)
     | *2*   : PP format (32 bit IEEE)
     | *3*   : GRIB format (Unblocked)
     | *4*   : GRIB format (Cray blocked)
     | *7*   : NetCDF format
     | *8*   : Grads format
     | *34*  : PP format (64 bit Real 32 bit Integer IEEE)
     | *65*  : UM format (64 bit IEEE)
     | *66*  : PP format (64 bit IEEE)
     | *165* : UM format (64 bit Cray)
     | *166* : PP format (Cray blocked 64 bit Cray)
     | *167* : PP format (Cray blocked 64 bit IEEE)
     | *201* : UM format (32 bit IEEE byte swapped)
     | *202* : PP format (32 bit IEEE byte swapped)
     | *265* : UM format (64 bit IEEE byte swapped) 
     | *266* : PP format (64 bit IEEE byte swapped)

**reset_trans**
     Reset transformation/interpolation variables to their default values.
     See the individual commands for the default values. 

**set_cal** *fieldlist calendar*
     For each of the fields in *fieldlist* set the calendar type. The value of
     *calendar* can be one of these strings "GREGORIAN", "gregorian", "360",
     "JULIAN", "julian", "NOLEAP" or "noleap" or it can be an integer value
     which represents a calendar type

     | *1*  : Gregorian calendar
     | *2*  : 360 day calendar
     | *14* : Julian calendar
     | *15* : No leap year calendar

**set_description** *fieldlist name*
     For each of the fields in *fieldlist* set the description string. For 
     netCDF files the description string will be written out as the *source*
     attribute, if selected.

**set_longname** *fieldlist name*
     For each of the fields in *fieldlist* set the long name string. For 
     netCDF files the long name string will be twritten out as the *long_name*
     or the *title* attribute, if selected.

**set_mdi** *fieldlist newmdi*
     For each of the fields in *fieldlist* set the missing data indicator value.
     This command can be used to correct the missing data indicator if it does 
     not match the actual missing data values.

**set_shortname** *fieldlist name*
     For each of the fields in *fieldlist* set the short name string. For 
     netCDF files the short name string will be written out as the 
     *short_name* attribute or the *name* attribute, if selected. It will also
     be used for the variable name.

**set_standardname** *fieldlist name*
     For each of the fields in *fieldlist* set the standard name string. For 
     netCDF files the standard name string will be written out as the 
     *standard_name* attribute, if selected.

**set_tlongname** *fieldlist name*
     For each of the fields in *fieldlist* set the time dimension long name string.

**set_tname** *fieldlist name*
     For each of the fields in *fieldlist* set the time dimension name string. 

**set_tstandardname** *fieldlist name*
     For each of the fields in *fieldlist* set the time dimension standard name string.

**set_tunit** *fieldlist name*
     For each of the fields in *fieldlist* set the time dimension unit string. 

**set_unit** *fieldlist name*
     For each of the fields in *fieldlist* set the unit string. For 
     netCDF files the unit string will be written out as the 
     *units* attribute, if selected.

**set_xlongname** *fieldlist name*
     For each of the fields in *fieldlist* set the x dimension long name string.

**set_xname** *fieldlist name*
     For each of the fields in *fieldlist* set the x dimension name string. 

**set_xstandardname** *fieldlist name*
     For each of the fields in *fieldlist* set the x dimension standard name string.

**set_xunit** *fieldlist name*
     For each of the fields in *fieldlist* set the x dimension unit string. 

**set_ylongname** *fieldlist name*
     For each of the fields in *fieldlist* set the y dimension long name string.

**set_yname** *fieldlist name*
     For each of the fields in *fieldlist* set the y dimension name string. 

**set_ystandardname** *fieldlist name*
     For each of the fields in *fieldlist* set the y dimension standard name string.

**set_yunit** *fieldlist name*
     For each of the fields in *fieldlist* set the y dimension unit string. 

**set_zlongname** *fieldlist name*
     For each of the fields in *fieldlist* set the z dimension long name string.

**set_zname** *fieldlist name*
     For each of the fields in *fieldlist* set the z dimension name string. 

**set_zstandardname** *fieldlist name*
     For each of the fields in *fieldlist* set the z dimension standard name string.

**set_zunit** *fieldlist name*
     For each of the fields in *fieldlist* set the z dimension unit string. 

**setdim** *dim fieldlist dimlist*
     Choose the values given by *dimlist* for the dimension given by 
     *dim*, for the fields in *fieldlist*. The value of *dim*
     should be one of *1*, *2*, *3* or *4* corresponding to
     the x, y, z and time dimensions.
     Currently convsh only allows dimension sub-sampling for the z and time
     dimensions, therefore *dim* should be either *3* or *4*. 
     As an example 
     suppose field number 2 has the following levels (1000,900,800,500,200,100)
     defined and only levels (1000,500,100) were needed, then the following 
     should be used: **setdim** *3 2 "0 3 5"*. 

**setdimatt** *attribute1 attribute2 attribute3 ... state*
     Set the state of netCDF dimension attributes. There is a special attribute
     *all* which will set all attributes to a particular state. This can be 
     useful to set a default attribute state, not used for example, then just 
     select the particular attributes you wish to include. Some attributes apply
     to all dimensions others only to a particular dimension.
     The values available for state are

     | *att_use*   : This attribute will be used for all relevant dimensions
     | *att_nouse* : This attribute will not be used for any dimensions
     | *att_cond*  : This attribute will be used only when there is data 
                     available or when the attribute value is different 
                     from the assumed default value.

**setglobatt** *attribute1 attribute2 attribute3 ... state*
     Set the state of netCDF global attributes. There is a special attribute
     *all* which will set all attributes to a particular state. This can be 
     useful to set a default attribute state, not used for example, then just 
     select the particular attributes you wish to include. The *history* 
     attribute is set internally by convsh and therefore can't be turned off.
     The values available for state are

     | *att_use*   : This global attribute will be used
     | *att_nouse* : This global attribute will not be used

**setgrid** *dim n v0 dv*
     Defines the new grid for the **interp_grid**, **spec_trans** or 
     **edit_grid** commands. The argument *dim* should have the value *1* if a 
     new x grid is being defined and the value *2* if a new y grid is 
     being defined. The
     argument *n* gives the number of points on the new grid. The argument 
     *v0* gives the first value of the new grid. The argument 
     *dv* gives the grid length of the new grid, *dv* should be
     negative if the grid values are decreasing. 

**setgridtype** *gridtype*
     Sets the new grid type for the **interp_grid** or **spec_trans**
     commands, *gridtype* has the value *regular* for
     a regular grid and the value *gaussian* for a Gaussian grid. If 
     **setgridtype** is not used **interp_grid** will interpolate to a 
     regular grid and **spec_trans** will transform to a Gaussian grid. 

**setinterp** *interp*
     Defines the interpolation method for **interp_grid**, *interp*
     is either *bilinear* for bilinear interpolation or 
     *area_weighted* for area weighted interpolation. 
     The default type of interpolation is bilinear. 

**setlsm** *lsm*
     Defines whether the input data to **interp_grid** is a land/sea mask,
     *lsm* is *true* if the data is a land/sea mask, 
     *false* otherwise. The 
     default value of *lsm* is *false*. 

**setmiss** *miss*
     Defines whether the input data to **interp_grid** contains missing
     data values, *miss* is *true* if the data contains missing
     data values, *false* otherwise. 
     The default value of *miss* is *false*. 

**setpole** *pole*
     Defines whether **interp_grid** will average polar data values,
     if *pole* is *true* then polar data will be averaged, 
     otherwise it will not. 
     The default value of *pole* is *false*. 

**setprecip** *precip1 precip2*
     Defines whether **interp_grid** will use a precipitation cutoff,
     if *precip1* is *true* then a precipitation cutoff value of 
     *precip2* will be used, otherwise no precipitation cutoff is used.
     The precipitation cutoff is implemented in two steps, firstly any output
     field value less than *precip2* will be set to zero. Secondly, for
     each output grid point, the nearest input field grid point is determined,
     if the value of precipitation at this latter point in the input data
     field is less than *precip2*, then the precipitation at the output
     grid point is set to zero.
     The default value of *precip1* is *false*. 

**setrotpole** *xpole ypole*
     If **interp_grid** is interpolating to a grid with a rotated pole,
     **setrotpole** should be used to set the new north pole longitude to
     *xpole* and the  new north pole latitude to *ypole*. By default
     *xpole* has the value *0.0* and *ypole* has the value 
     *90.0* i.e. an unrotated grid. 

**settrunc** *nspec*
     Defines the output truncation for **spec_trunc**. The command will
     also set up the equivalent Gaussian grid for T *nspec* truncation,
     which can be used by the **interp_grid**, **spec_trans** and **edit_grid** 
     commands. 

**setvaratt** *attribute1 attribute2 attribute3 ... state*
     Set the state of netCDF variable attributes. There is a special attribute
     *all* which will set all attributes to a particular state. This can be 
     useful to set a default attribute state, not used for example, then just 
     select the particular attributes you wish to include. The values available 
     for state are

     | *att_use*   : This attribute will be used for all variables
     | *att_nouse* : This attribute will not be used for any variables
     | *att_cond*  : This attribute will be used only when there is data 
                     available or when the attribute value is different 
                     from the assumed default value.

**spec_trans** *fieldlist*
     Transform spectral data onto a grid, for fields in *fieldlist*.
     The initial spectral coefficients will either come from the input data
     or from a previous **spec_trunc** command. If a grid is not
     defined using **setgrid** or **settrunc**, then the 
     equivalent Gaussian grid for the input spectral truncation will
     be used. 

**spec_trunc** *fieldlist*
     Truncate spectral data, for fields in *fieldlist*, 
     by chopping off the small wavelength coefficients.
     The initial spectral coefficients will either come from the input data
     or from a previous **spec_trunc** command. The output truncation is 
     defined using **settrunc**. 

**writefile** *filetype filename fieldlist*
     Write out the fields in *fieldlist* to file *filename* of type
     *filetype*. The argument *filetype* can be one of
     *netcdf* or *grads*. 

**writeglobatt** *attribute value*
     write *value* into the global attribute *attribute*

**zonal_mean** *fieldlist*
     For each of the fields in *fieldlist* calculate the zonal mean.

