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

If you use `set textwidth=72` or similar in your `~/.vimrc`, you'll most
likely want to have a look at the shipped `textios.vim`: It resets the
text width to zero (unlimited) for textios. You don't want to wrap lines
when using textios – this will break everything.

Refer to textios's manpage for a full list of command line options and
interactive commands.


htmlios
=======

htmlios uses the same configuration as textios. While textios is meant
for interactive use, htmlios will render HTML files. Large fonts. Stuff
like that. Suitable for your displaying your monitoring in your office.

htmlios is able to do more filtering than textios can:

	htmlios -e host1,host2 -o UPDATES -s WARNING,CRITICAL

`host1` and `host2` will be skipped, only updates will be shown, only
the states `WARNING` and `CRITICAL` will be shown.

htmlios is able to save intermediate CSV output:

	htmlios [...] -C foo.csv

Later on, you can generate multiple HTML files from this data:

	htmlios -o UPDATES [...] -c foo.csv -O updates.html
	htmlios -o 'DISK SPACE' [...] -c foo.csv -O disks.html

You can also combine data from multiple Icinga/Nagios instances:

	htmlios -C location1.csv location1
	htmlios -C location2.csv location2
	htmlios -C location3.csv location3

	cat location{1,2,3}.csv >all.csv

	htmlios -c location1.csv -O location1-everything.html
	htmlios -c all.csv -o UPDATES -O all-updates.html

See? You only need to download your data once.

Refer to htmlios's manpage for a full list of command line options.


Configuration
=============

See `man textiosrc`.


Disclaimer
==========

These tools fit my needs. They are not universal tools that will please
everyone – and they never will be.


TODOs
=====

- Use Icinga's REST API
