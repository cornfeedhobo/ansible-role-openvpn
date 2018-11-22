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
| `openvpn_service` | `false` |
| `openvpn_service_state` | `"started"` |
| `openvpn_service_enabled` | `true` |
| `openvpn_service_name` | `"{{ __openvpn_service_name }}"` |
| `openvpn_user` | `"openvpn"` |
| `openvpn_group` | `"openvpn"` |
| `openvpn_config_dir` | `"/etc/openvpn"` |
| `openvpn_config` | `{}` |

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
           openvpn_name: "server"
           openvpn_config:
             key: "{{ lookup('file', 'foobar.key') }}"
             cert: "{{ lookup('file', 'foobar.crt') }}"
             ca: "{{ lookup('file', 'ca.crt') }}"
             dh: "{{ lookup('file', 'dh.key') }}"
             port: 1194
             proto: "udp"
             dev: "tun"
             persist-tun: ""
             server: "172.16.16.0 255.255.255.0"
             ifconfig-pool-persist: "ipp.txt"
             max-clients: "10"
             keepalive: "10 120"
             comp-lzo: "yes"
             client-to-client: ""
             persist-key: ""
             log-append: "/var/log/openvpn.log"
             mute: 20
             verb: 3

License
-------

MIT
