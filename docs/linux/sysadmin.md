
# Linux System Administration

## Delete files older than x days


Here is a simple command to delete all files in given folder, older than x days:

  find /path/to/files* -mtime +5 -exec rm {} \;

Note that there are spaces between rm, {}, and \;


## References

[[http://www.thegeekstuff.com/2014/01/linux-sysadmin-books|The geek stuff - 10 Essential Linux System Administration Books]]