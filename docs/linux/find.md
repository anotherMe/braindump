# find

## Find files with name like

  $ find /my/target/folder -name "*.pdf" -type f


## Find files newer than / older than

Find all files in current folder newer than 01/01/2015:

  find . -newermt 20150101


Find all files in current folder older than 01/01/2015:

  find . -not -newermt 20150101
  
Find all files modified more than 60 days ago:

  find . -mtime +60