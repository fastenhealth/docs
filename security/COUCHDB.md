> https://github.com/mitre/apache-couchdb-srg-baseline/issues/4

When testing controls the following actions were taken to harden the security and allow the tests to pass.

1. The following lines were uncommented and the values were set as given:
	Set SSL enabled to be true in the [ssl] section of local.ini
	Set cert file path to cert_file = /etc/couchdb/cert/couchdb.pem in the [ssl] section of local.ini
	Set key file path to key_file = /etc/couchdb/cert/privkey.pem in the [ssl] section of local.ini
	Set cert_ca file path to cacert_file = /etc/ssl/certs/ca-certificates.crt in the [ssl] section of local.ini
	Set log write_delay =0 in the [log] section of default.ini 
	Set log syslog_facility to local [0-7] in the [log] section of default.ini 
	Set ssl secure renegotiate to true in the [ssl] section of local.ini
	Set file = ./couch.log in the [log] section of default.ini 

2. The following commands were run to set the privileges for the configuration files
	$ sudo chmod 640 /opt/couchdb/etc/local.ini
	$ sudo chmod 640 /opt/couchdb/etc/default.ini

3. The following commands were run to generate key
	$ sudo mkdir /etc/couchdb/cert/
	$ sudo chmod 700 cert/
	$ cd /etc/couchdb/cert/
	$ sudo openssl genrsa > privacy.pem
	$ sudo chmod 600 privkey.pem
	$ sudo chown couchdb privacy.pem couchdb.pem
	
