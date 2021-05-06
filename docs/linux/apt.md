# apt

## List all installed packages

  dpkg --get-selections | grep -v deinstall
  
## List of files provided from installed package

  dpkg-query -L <package_name>
  
## List of files provided from not-installed package

  [[http://packages.ubuntu.com]]