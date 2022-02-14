tls_cert
=========

Deploys TLS server certificates and their corresponding CA certificate chain
onto a host.

Certificates from the [TCS service](https://security.geant.org/trusted-certificate-services/)
can be OV (Organization Validated) or EV (Extended Validation) certificates. This role deploys:

* the key pair
* the chain that belongs to it
* a single file containing private key, cert, and chain

TODO: generate pkcs12/jks key stores based on defined keystore password.


Requirements
------------

Ansible 3.0+

Role Variables
--------------


```yaml
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
```

It is advisable to use `ansible-vault` or similar to encrypt your private key.


Example Playbook
----------------

```yaml
- hosts: servers
  become: true
  roles:
    - role: ansible_role_tls_cert
      vars:
        tls_cert_restart_services:
          - apache2
          - postgresql
          - postfix
```


License
-------

BSD

Author Information
------------------

Dick Visser <dick.visser@geant.org>
