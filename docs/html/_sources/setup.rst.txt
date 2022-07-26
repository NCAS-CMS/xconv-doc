.. _setup:

Setup xconv windows
===================

Clicking on the **Setup** button in the main xconv window brings up a menu
window to select one of four xconv setup options.

.. image:: images/xconv_1.93_setup_menu.png
   :alt: Setup xconv menu window

Each of the four setup windows have the same five buttons along the bottom row,
these buttons have the following functions.
**Apply** applies any changes to the current xconv session only.
**Save** applies any changes to the current xconv session and writes them 
to a file called .xconvrc in your home directory. This file is read every time
xconv is started, hence any changes made will become permanent.
**Default** resets xconv back to a default state.
**Reset** resets xconv back to the state it was in when **Apply** or
**Save** was last clicked.
**Dismiss** removes the setup window.

.. _setup_defaults:

Setup xconv defaults window
---------------------------

.. image:: images/xconv_1.93_setup_defaults.png
   :alt: Setup xconv defaults window

This window is used to customise various aspects of xconv, including fonts,
colours and output options.


.. _setup_stash:

Setup STASH master files window
-------------------------------

.. image:: images/xconv_1.93_setup_STASHmaster.png
   :alt: Setup STASH master files window

Xconv has internally stored information extracted from Unified Model STASHmaster
files, this window allows additional user STASHmaster files to be added. This
enables xconv to display the correct field title for unknown STASH codes. Xconv includes information from STASHmaster files for model versions 4.0 - 10.2.

.. _setup_netcdf_att:

Setup netCDF attributes window
------------------------------

.. image:: images/xconv_1.93_setup_netcdf_att.png
   :alt: Setup netcdf attributes window

Select the netCDF attributes to include when xconv writes netCDF files. The 
**cond** option means xconv will only include this attribute when there is data
available or when the attribute value is different from the assumed default 
value.

.. _setup_netcdf_glob_att:

Setup netCDF global attributes window
-------------------------------------

.. image:: images/xconv_1.93_setup_netcdf_glob_att.png
   :alt: Setup netcdf global attributes window


Select the global netCDF attributes to include when xconv writes netCDF files
and enter the attribute string you wish to see written. All global netCDF
attributes are optional except **history** which has a default value of ::

   :history = "Thu Oct 15 16:37:17 BST 2015 - XCONV V1.93 13-October-2015" ;

The first part of the string will be the date and time the netCDF file was 
written and the second part is the xconv version used and the release date for
this version. Any **history** attribute added in this window will be appended
to the above string.
