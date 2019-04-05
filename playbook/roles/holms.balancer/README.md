# balancer [![Build Status](https://travis-ci.org/holms/ansible-balancer.svg?branch=master)](https://travis-ci.org/holms/ansible-balancer)

Load Balancer with nginx role.

This role is only for SSL termination setup. Everything from HTTP will be redirected to HTTPS. You can fork and change that or you can contribute to make this optional.

## Requirements

Latest Ansible from pip

## Platforms

- Ubuntu
- Debian

## Role Variables

Name                     | Default                                                                                                                                              | Value
:----------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- | :-----------------------------------------------
balancer_vhosts          | - { name: "example1",  upstreams: ['myserver1.com', 'myserver2.com' ] } <br> - { name: "example2",  upstreams: ['myserver1.com', 'myserver2.com' ] } | a list of vhosts
balancer_ssl_key         | *None*                                                                                                                                               | Path to SSL key
balancer_ssl_pem         | *None*                                                                                                                                               | Path to PEM file
balancer_ssl_crt         | *None*                                                                                                                                               | Path to CRT file
balancer_ssl_trusted_crt | *None*                                                                                                                                               | Path to CRT file of your trusted ssl certificate
balancer_ssl_trusted_key | *None*                                                                                                                                               | Path to KEY file of your trusted ssl certificate
listen | "80 http2" | listen's value at main server block
server_name | "yourserver.com" | server_name's value
error_page | false | error_page's value
port | None | Port's value used at error_page
server_without_port | false | Switch second server block on. It used for a site with SSL and without any specific port.

You need to use either trusted certificates or self signed, using will fail your nginx config

## Example. Without specific port

    - hosts: localhost
      remote_user: root
        - include_role:
            name: holms.balancer
          vars:
            balancer_vhosts:
              - name: codesearch
                upstreams: [ 's1.codesearch.aelve.com' ]
                listen: "{{ codesearch_port }} ssl"
                server_name: "codesearch.aelve.com"
                error_page: false
                server_without_port: true

## Example. With specific port

    - hosts: localhost
      remote_user: root
        - include_role:
            name: holms.balancer
          vars:
            balancer_vhosts:
              - name: codesearch-portainer
                upstreams: [ 's1.staging.codesearch.aelve.com:{{ codesearch_portainer_port }}' ]
                listen: "{{ codesearch_portainer_port }} ssl"
                server_name: "staging.codesearch.aelve.com"
                port: "{{ codesearch_portainer_port }}"
                error_page: true
                server_without_port: false

Or generate `upstreams` list from inventory vars group.

## License

MIT

## Author Information

Roman Gorodeckij ([holms@holms.lt](mailto:holms@holms.lt))
