# rsync

## One way synchronization

  rsync -av /path/to/source /path/to/destination

Where:

* **-a, --archive** - This is equivalent to -rlptgoD. It is a quick way of saying you want recursion and want to preserve almost everything (with -H being a notable omission). The only exception to the above equivalence is when --files-from is specified, in which case -r is not implied.
* **-v, --verbose**

Other, interesting options:

* **-u, --update** - This forces rsync to skip any files which exist on the destination and have a modified time that is newer than the source file. (If an existing destination file has a modification time equal to the source file's, it will be updated if the sizes are different.)
Note that this does not affect the copying of symlinks or other special
files. Also, a difference of file format between the sender and receiver is always considered to be important enough for an update, no matter what date is on the objects. In other words, if the source has a directory where the destination has a file, the transfer would occur regardless of the timestamps.
This option is a transfer rule, not an exclude, so it doesn't affect the
data that goes into the file-lists, and thus it doesn't affect deletions. It just limits the files that the receiver requests to be transferred.