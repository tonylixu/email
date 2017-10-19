## Introduction
A fullstack but simple mail server (smtp, imap, antispam, antivirus...).
Only configuration files, no SQL database. Keep it simple and versioned.
Easy to deploy and upgrade.

Includes:

- postfix with smtp or ldap auth
- dovecot for sasl, imap (and optional pop3) with ssl support, with ldap auth
- saslauthd with ldap auth
- amavis
- spamassasin supporting custom rules
- clamav with automatic updates
- opendkim
- opendmarc
- fail2ban
- fetchmail
- postgrey
- basic [sieve support](https://github.com/tomav/docker-mailserver/wiki/Configure-Sieve-filters) using dovecot
- [LetsEncrypt](https://letsencrypt.org/) and self-signed certificates
- persistent data and state (but think about backups!)
- [integration tests](https://travis-ci.org/tomav/docker-mailserver)
- [automated builds on docker hub](https://hub.docker.com/r/tvial/docker-mailserver/)
