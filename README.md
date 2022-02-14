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
# PEM formatted X.509 certificate
# tls_cert_crt:
# PEM formatted X.509 private key
# tls_cert_key:

# Key vars
tls_cert_key_dest_dir: /etc/ssl/private
tls_cert_key_dest_name: server.key
# all-in-one file name (key+crt+chain)
tls_cert_allinone_dest_name: server.pem
tls_cert_key_owner: root
tls_cert_key_group: ssl-cert
tls_cert_key_mode: 0640

# Cert vars
tls_cert_crt_dest_dir: /etc/ssl/certs
tls_cert_crt_dest_name: server.crt
tls_cert_full_dest_name: server_full.crt
tls_cert_crt_owner: root
tls_cert_crt_group: root
tls_cert_crt_mode: 0644

# CA vars
tls_cert_ca_alias: chain.crt

# Reload services upon changes
tls_cert_reload_services: []
# tls_cert_reload_services:
#   - apache2
#   - postfix
#   - postgresql
#   - nginx
```



It is advisable to use `ansible-vault` or similar to encrypt your private key.


Example Playbook
----------------

```yaml
- hosts: myserver
  become: true
  roles:
    - role: ansible_role_tls_cert
      vars:
        tls_cert_crt: |
          -----BEGIN CERTIFICATE-----
          MIIBkTCCATegAwIBAgIUc9C1CPsz7HvWYeeeCZKPjtB/RSkwCgYIKoZIzj0EAwIw
          HjEcMBoGA1UEAwwTZ2l0aHViLWRlbW8ta2V5cGFpcjAeFw0yMjAyMTQxMjI2MzJa
          Fw0zODAxMTcxMjI2MzJaMB4xHDAaBgNVBAMME2dpdGh1Yi1kZW1vLWtleXBhaXIw
          WTATBgcqhkjOPQIBBggqhkjOPQMBBwNCAATivAvRWOtdjXxCB8DAEs65jArkLdti
          q5goH9bmZ/p/+KLWAHaXAYBhrZv7+SSrwD3tvCqpY9iFh9ZliifOBA4qo1MwUTAd
          BgNVHQ4EFgQUOhDZkevX/EQQGoLQ3NNaEe3RPfswHwYDVR0jBBgwFoAUOhDZkevX
          /EQQGoLQ3NNaEe3RPfswDwYDVR0TAQH/BAUwAwEB/zAKBggqhkjOPQQDAgNIADBF
          AiAywXHOtuwTDFuuJJAkIkhUNZIsXJeM5ahcTFJreSS/jwIhANsxaApk3ZTDaTTP
          GtO4FXcc9ErXjjBZcSU8165lHMFG
          -----END CERTIFICATE-----
        tls_cert_key: |
          -----BEGIN PRIVATE KEY-----
          MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgl2A5ivqCUWowxKji
          ss76xTmPDCWumExO8v9srPEArYWhRANCAATivAvRWOtdjXxCB8DAEs65jArkLdti
          q5goH9bmZ/p/+KLWAHaXAYBhrZv7+SSrwD3tvCqpY9iFh9ZliifOBA4q
          -----END PRIVATE KEY-----
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
