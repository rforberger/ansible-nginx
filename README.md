# Ansible Nginx

Data:

```nginx:
mod_security: True
mod_security_compile: False
virtual_hosts:
- name: "test.ronnyforberger.de"
public_site: True
listeners_http:
- { ip: "{{ ansible_eth0.ipv4.address }}", port: '80' }
- { ip6: "{{ ansible_eth0.ipv6[0].address }}", port: '80' }
listeners_https:
- { ip: "{{ ansible_eth0.ipv4.address }}", port: '443' }
- { ip6: "{{ ansible_eth0.ipv6[0].address }}", port: '80' }
certificate_name: "{{ letsencrypt_dir }}/test.ronnyforberger.de/fullchain.pem"
key_name: "{{ letsencrypt_dir }}/test.ronnyforberger.de/privkey.pem"
is_default_server: false
mod_security: 'On'
mod_php: 'Off'
custom_server_name_port: False
tls_protocols: "TLSv1.2 TLSv1.3"
request_client_certificate: 'Off'
client_max_body_size: '100m'```