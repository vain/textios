textios
=======

Provides access to the most important parts of Icinga and Nagios:

 - Overview of current problems
 - ACKing problems
 - Scheduling downtimes (hosts and services)

textios uses Vim as its user interfaces. You get a list of services like
this:

	  haj2.config-slave      BACULA-DIR PROCESS         OK  PROCS OK: 1 process with command name bacula-dir''  
	  haj2.config-slave      BACULA-FD PROCESS          OK  PROCS OK: 1 process with command name bacula-fd''   
	  haj2.config-slave      BACULA-SD PROCESS          OK  PROCS OK: 1 process with command name bacula-sd''   

You can then prefix each line with a command, for example:

	hdown +2 Host down for the next two hours   haj2.config-slave      BACULA-FD PROCESS          OK  PROCS OK: 1 process with command name bacula-fd''   

Do a `:wqa` and you're done. The `a` in `:wqa` is most probably needed
because textios will open one Vim window for each of your Icinga/Nagios
instances.

Note the non-breaking spaces that are used as field separators.

textios uses curl to retrieve data. If you need to specify any
credentials, do so in your `~/.netrc`.

Refer to textios's manpage for a full list of command line options and
interactive commands.


htmlios
=======

While textios is meant for interactive use, htmlios will render HTML
files. Large fonts. Stuff like that. Suitable for your displaying your
monitoring in your office.

htmlios won't download any information. Instead, there's a special
switch for textios to save its internal data:

	textios -a -c /tmp/raw-textios-data

This creates a directory `/tmp/raw-textios-data` and, for each location,
a subdirectory. Actually, you don't need to know the gory details.
htmlios will simply pick up that data.

After you've downloaded that stuff, htmlios renders your html pages:

	htmlios -E UPDATES UPTIME -t 'Office' office1 office2 >office.html
	htmlios -o UPDATES UPTIME -t 'Updates' office2 colo >updates.html

Refer to the manual page of htmlios for a full list of options.

The point is: textios downloads all information *once*. htmlios is then
able to render multiple views on that data.


Configuration
=============

See `man textiosrc`.


Compatibility
=============

textios and htmlios are developed on Arch Linux. They have the following
dependencies:

 - awk
 - bash
 - curl
 - python2 (Python 2.7, actually)
 - vim

Some quick testing on OpenBSD 5.3 has been done, so textios/htmlios
should work on that system as well. (Probably other BSDs are fine, too,
but I haven't tried.)


Disclaimer
==========

These tools fit my needs. They are not universal tools that will please
everyone – and they never will be.
