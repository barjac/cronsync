# cronsync
cronsync is a bash script for syncing a local repository from Mageia mirrors using rsync.
When the failure of a first tier mirror almost caused my local repo to be wiped I 
wrote this little script which does the following:

* Checks the accessibility and file count of the first mirror in the 'mymirrors' variable in the scrit.
* If the file count on the mirror has dropped by more than a preset limit then other 
  mirrors are checked until a good one (or none) is found.

On finding a good mirror cronsync uses rsync to sync the repo from the mirror.

Any failures are reported in ~/cronsync_error.log
A copy of the last successful update output is saved in ~/cronsync_last.log
A list of file counts for all mirrors used is saved in ~/cronsync_file_count.log

To run as a cron job at ten past every hour use:
$ crontab -e
and set for example:
10 * * * *     $HOME/cronsync  (maybe best to avoid "0" ;)
