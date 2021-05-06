# Icinga 2

## Icinga 2 installation

Installation instructions for Icinga 2 on a Ubuntu Server 16.04 minimal installation.

For detailed informations refer to:

[[https://docs.icinga.com/icinga2|Icinga2 Documentation]]
[[https://github.com/Icinga/icingaweb2/blob/master/doc/02-Installation.md|Icinga GitHUB Readme]]


In order to perform all the following installation tasks you have to add Icinga repository:

  # add-apt-repository ppa:formorer/icinga
  # apt-get update

Install Icinga 2:

  # apt-get install icinga2

Icinga relies on the Nagios check plugins, so:

  # apt-get install nagios-plugins

Start Icinga:

  # /etc/init.d/icinga2 start


## Icinga Web 2 installation


## Database setup

Between MySQL and PostgreSQL, we choose the latter one:

  # apt-get install postgresql
  # apt-get install icinga2-ido-pgsql

During //icinga2-ido-pgsql// installation process you'll be asked for PostgreSQL automatic database configuration. Refer to Icinga documentation for manual configuration.


### Apache and PHP installation

Set up Apache and PHP:

  # apt-get install apache2
  # apt-get install php libapache2-mod-php php-pgsql php-gettext php-intl php-curl
  # service apache2 restart

Set PHP timezone by editing file **/etc/php/7.0/apache2/php.ini**. Add / edit line:

  date.timezone = Europe/Rome

then restart Apache.


Enable external command pipe:

  # icinga2 feature enable command
  # service icinga2 restart

Add your webserver's user to the group //**icingacmd**// ( //**nagios**// on Debian ) to enable sending commands to Icinga 2 through your web interface:

  # usermod -a -G nagios www-data

Add repository:

  $ wget -O - http://packages.icinga.org/icinga.key > icinga.key
  $ sudo apt-key add icinga.key
  $ sudo add-apt-repository 'deb http://packages.icinga.org/ubuntu icinga-xenial main'
  $ sudo apt-get update

Install Icinga Web 2:

  # apt-get install icingaweb2

### Web Setup Wizard

You can set up Icinga Web 2 quickly and easily with the Icinga Web 2 setup wizard which is available the first time you visit Icinga Web 2 in your browser. When using the web setup you are required to authenticate using a token. In order to generate a token use the icingacli:

  icingacli setup token create

In case you do not remember the token you can show it using the icingacli:

  icingacli setup token show
  
Finally visit Icinga Web 2 in your browser to access the setup wizard and complete the installation: 

  http://YOURSERVERIP/icingaweb2/setup


### Database Setup

During the web setup wizard procedure, you'll be asked to create a database for storing users and groups ( stated you haven't choose to use LDAP or something else ). This one has nothing to do with the database you created previously.


