Using the [[http://manpages.ubuntu.com/manpages/maverick/man8/pg_createcluster.8.html|pg_createcluster]] command that comes with the debian/ubuntu postgres packages:

Delete current cluster, if it does not contain any prior data:

  # pg_dropcluster --stop 9.6 main

Create a new cluster at the new location:

  # pg_createcluster -d /path/to/new/location 9.6 main

Restart postgresql:

  # systemctl restart postgresql


