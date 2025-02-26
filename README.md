# Ansible Nginx

Data:

```
nginx:
  mod_security: True
  mod_security_compile: False
  virtual_hosts:
    - name: "groupware.forberger-online.de"
      public_site: True
      target_servers:
        - { hostname: "[::1]", port: "8080", protocol: "http" }
      listeners_http:
        - { ip: "{{ ansible_eth0.ipv4.address }}", port: '80' }
        - { ip: "[{{ ansible_eth0.ipv6[0].address }}]", port: '80' }
      listeners_https:
        - { ip: "{{ ansible_eth0.ipv4.address }}", port: '443' }
        - { ip: "[{{ ansible_eth0.ipv6[0].address }}]", port: '443' }
      certificate_name: "{{ letsencrypt_dir }}/groupware.forberger-online.de/fullchain.pem"
      key_name: "{{ letsencrypt_dir }}/groupware.forberger-online.de/privkey.pem"
      is_default_server: true
      mod_security: 'On'
      mod_php: 'Off'
      custom_server_name_port: False
      tls_protocols: "TLSv1.2 TLSv1.3"
      request_client_certificate: 'Off'
      client_max_body_size: '100m'
      client_certificate: 'client.crt'
```