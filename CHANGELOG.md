# Change log

## Version 1.0.6

### New Features

* Added support for installation on the RHEL 9 family
* Added GPG keys for epel-release, onlyoffice, and nginx
* Added the ability to set up JWT secrets
* Added the ability to customize values in the ONLYOFFICE Docs configuration
* Added the ability to install onlyoffice-documentserver RPM package by URL
* Added the ability to set up a custom document-server port
* Added the option to configure an allowed IP/CIDR network for the info page
* Added the ability to set up the ONLYOFFICE Docs's package state to the latest or present

### Fixes

* Fixed [issue](https://github.com/ONLYOFFICE/ansible-role-documentserver/issues/67) by changing supervisorctl to systemctl
* Updated service names
* Fixed installation on RedHat 7
* Fixed [issue](https://github.com/ONLYOFFICE/ansible-role-documentserver/issues/43) with JWT configuration on Debian
* Updated example playbook
* Updated repository links
* Added `log_directory` postgresql variable to fix [issue](https://github.com/geerlingguy/ansible-role-mysql/issues/175)
