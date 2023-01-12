# Change log

## Version 1.0.6

### New Features

* Added the ability to set up JWT secrets
* Added the ability to change values in documentserver config with user custom values
* Added the ability to install RPM package of onlyoffice-documetserver by URL
* Added the ability to set up custom documentserver port
* Added the option to configure a 'allow' IP/CIDR network for the info page
* Added the ability to set up documentserver package state latest | present

### Fixes

* Fix [issue](https://github.com/ONLYOFFICE/ansible-role-documentserver/issues/43) with JWT configure on Debian
* Updated padding in sample playbook
* Repository links updated for a more secure connection
* Added `log_directory` postgresql variables for fix typical [issue](https://github.com/geerlingguy/ansible-role-mysql/issues/175),
  and the correct operation of the dependent role
