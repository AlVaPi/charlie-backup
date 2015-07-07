What if you have a lot of files to back up? There are many efficient pieces of software (rsync, bacula, etc.) but the problem is that they have so high requirements that often backup server will cost you more then your production one with all the data and running projects.

This simple PHP package allows you to do practically the same as other serious ones but it doesn't need a lot of expertise to set it up and need only basically equipped backup host (may be even just a netdrive at office/home).

The package may be useful for SME providers. It can handle decades (and may be even hundreds) of gigabytes of data and takes niche where simple file copying to a remote host already don't work but other existing solutions look too hefty.

Features
Transfers only updated files
Keeps multiple rotating backup copies
Identical copies do not take extra disk space
Very large files transferred in chunks
Dumps MySQL databases to backup them too
Doesn't need shell access
Specific Requirements
Source host
PHP 4+
cron
MySQL (optionally)
Backup host
UNIX based OS
Web server
PHP 4+ (safe mode is OK)
Installation
Package consists of three PHP scripts:

Sender - placed at source host and called with cron daily
Dumper - optionally placed at source host and called with cron daily
Receiver - placed at backup host within web access area
Sender
Upload script to what ever convenient location at the source host. Open it with a text editor and find commented configuration lines in the beginning of the script. Edit those lines to match your needs.

Set up cron job which run this script (CLI or wget) once a day.

Dumper
Do the same as with Sender. This script only need if you would like to backup MySQL databases. It should create files in the same pool with other files intended to backup later by Sender. Any other utility instead of this one can be used too. Dumper is just more intelligent than MySQL stock utility. In fact this component can be used separately to sort out multiple MySQL dumps. It processes only updated tables and has filter for certain databases and tables, may store dumps to specific locations.

Receiver
Prepare directory to hold your backup and assign proper attributes to this directory in order Receiver may create and delete files there.

Upload script to web area at the backup host so that it can be called by HTTP from outer world. Open script file with a text editor and find commented configuration lines in the beginning of the script. Edit those lines to match your needs. You may test it by calling the script with a web browser.

That's all.
