tls_cert
=========

Deploys TLS server certificates and their corresponding CA certificate chain to a host.

Certificates from the TCS service are either regular (i.e. Domain Validated) certificates, or EV (Extended Validation) certificates. 
This role deploys:

* the key pair
* the chain that belongs to it
* a single file containing private key, cert, and chain

TODO: generate pkcs12/jks key stores based on defined keystore password.


Requirements
------------

OpenSSL

Role Variables
--------------

A hosts' host_vars should contain these two vars contain the certificate and the private key:

```
tls_cert_crt: |
 -----BEGIN CERTIFICATE-----
  MIIEYzCCA0ugAwIBAgIQBp43Tw4JNie9o9zO/cKbCzANBgkqhkiG9w0BAQ0FADBk
  MQswCQYDVQQGEwJOTDEWMBQGA1UECBMNTm9vcmQtSG9sbGFuZDESMBAGA1UEBxMJ
  QW1zdGVyZGFtMQ8wDQYDVQQKEwZURVJFTkExGDAWBgNVBAMTD1RFUkVOQSBTU0wg
  Q0EgMzAeFw0xNjExMjgwMDAwMDBaFw0xOTEyMDMxMjAwMDBaMHMxCzAJBgNVBAYT
  Ak5MMRYwFAYDVQQIEw1Ob29yZC1Ib2xsYW5kMRIwEAYDVQQHEwlBbXN0ZXJkYW0x
  GzAZBgNVBAoMEkfDiUFOVCBBc3NvY2lhdGlvbjEbMBkGA1UEAxMSd2lraS11YXQu
  Z2VhbnQub3JnMFkwEwYHKoZIzj0CAQYI..... etc
  -----END CERTIFICATE-----

tls_cert_key: |
  -----BEGIN PRIVATE KEY-----
  MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgQn3F4SqdSOARpOd2
  5YcHDPZh6bIpb79BRdHONCAASx1IjoG......etc
  -----END PRIVATE KEY-----

It is advisable to use `ansible-vault` or similar to encrypt your private key.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------


    - hosts: servers
      become: true
      roles:
        - tls_cert
      

License
-------

BSD

Author Information
------------------

Dick Visser <dick.visser@geant.org>
