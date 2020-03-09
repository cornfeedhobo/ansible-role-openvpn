openvpn [![Ansible Role](https://img.shields.io/ansible/role/d/33270.svg)](https://galaxy.ansible.com/cornfeedhobo/openvpn)
=======

Install, configure, and manage OpenVPN

    ansible-galaxy install cornfeedhobo.openvpn

Role Variables
--------------

|Name|Default Value|
|-|-|
| `openvpn_install` | `false` |
| `openvpn_packages` | `"{{ __openvpn_packages }}"` |
| `openvpn_package_state` | `"present"` |
| `openvpn_configure` | `false` |
| `openvpn_config_dir` | `"{{ __openvpn_config_dir }}"` |
| `openvpn_config` | `{}` |
| `openvpn_owner` | `"openvpn"` |
| `openvpn_group` | `"openvpn"` |
| `openvpn_mode` | `"0600"`
| `openvpn_name` | `"server"` |
| `openvpn_service` | `false` |
| `openvpn_service_state` | `"started"` |
| `openvpn_service_enabled` | `true` |
| `openvpn_service_name` | `"{{ __openvpn_service_name }}"` |

`openvpn_config` is a special directive to map [openvpn config values](https://openvpn.net/community-resources/reference-manual-for-openvpn-2-4/)
directly into the openvpn.conf format. To work around openvpn's config's
support for duplicate keys and valueless keys, this directive accepts lists
for duplicate keys, and empty strings for valueless keys. Additionaly, values
requiring quoting in openvpn.conf must be double quoted in your playbook.
Please see the [Example Playbook](#example-playbook) for working examples.

Dependencies
------------

- [cornfeedhobo.epel](https://github.com/cornfeedhobo/ansible-role-epel)

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: cornfeedhobo.openvpn
          openvpn_install: true
          openvpn_configure: true
          openvpn_service: true
          openvpn_config:
            tls-server: ""
            tls-crypt: "{{ lookup('file', 'tlsauth.key') }}"
            key: "{{ lookup('file', 'ssl.key') }}"
            cert: "{{ lookup('file', 'ssl.crt') }}"
            ca: "{{ lookup('file', 'ca.crt') }}"
            dh: "{{ lookup('file', 'dh.key') }}"
            persist-key: ""
            dev: "tun"
            persist-tun: ""
            port: 1194
            proto: "udp"
            server: "172.222.222.0 255.255.255.0"
            server-ipv6: "fd00::ffff:acde:de00/112"
            ifconfig-pool-persist: "ipp.txt"
            max-clients: "10"
            keepalive: "10 120"
            client-to-client: ""
            push:
              - '"redirect-gateway def1"'
              - '"dhcp-option DNS 8.8.8.8"'
              - '"dhcp-option DNS 8.8.4.4"'
              - '"dhcp-option DNS 2001:4860:4860::8888"'
              - '"dhcp-option DNS 2001:4860:4860::8844"'
            log-append: "/var/log/openvpn.log"
            mute: 20
            verb: 3

License
-------

MIT
