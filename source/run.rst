.. _run:

Running Convsh scripts
======================

There are two methods to run convsh scripts, the first method is to directly use
the executable: ::

   convsh script.tcl

where *script.tcl* should be replaced with the name of your script. The above
only works if convsh is in your $PATH. It could be the case there is no convsh
executable or it could be an older version of the code, in this case use ::

   convsh1.93 script.tcl

If convsh is not in your $PATH then use the full pathname, for example ::

   /home/umui/umtools/linux_x86_64/bin/convsh1.93 script.tcl

The second method of running a convsh script is to use the first line in the 
script to specify the executable to run. If convsh is in your $PATH then use ::

   #! /usr/bin/env convsh

or ::

   #! /usr/bin/env convsh1.93

If convsh is not in you $PATH then use the full pathname, for example ::

   #!/work/n02/n02/hum/bin/convsh

If you use this method to run convsh scripts then the script must have
execute mode set, to do this run ::

   chmod +x script.tcl

Finally to run the script type ::

   ./script.tcl
