# ansible-firewalld

[![Build Status](https://travis-ci.org/shhirose/ansible-firewalld.svg?branch=master)](https://travis-ci.org/shhirose/ansible-firewalld)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

This is Ansible role for firewalld install and setting for RedHat Enterprise Linux.

## Requirements

None

## Role Variables Sample

```yaml
shhirose_firewalld:
  default_zone: public

  zones:
    - zone: test1
      state: enabled

  interfaces:
    - interface: eth901
      zone: public
      immediate: yes
      permanent: True
      state: enabled

  targets:
    - target: DROP
      zone: home

  masquerades:
    - masquerade: yes
      zone: public
      immediate: yes
      permanent: True

  services:
    - service: http
      zone: public
      immediate: yes
      permanent: True
      state: enabled

  ports:
    - port: "8080/tcp"
      zone: public
      immediate: yes
      permanent: True
      state: enabled

  rich_rules:
    - rule: "rule family="ipv4" source address="192.168.0.0/16" port protocol="tcp" port="22" accept"
      zone: public
      immediate: yes
      permanent: False
      state: enabled

  icmp_blocks:
    - type: echo-request
      zone: public
      immediate: yes
      permanent: False
      state: enabled

  sources:
    - source: "172.10.0.0/16"
      zone: public
      immediate: yes
      permanent: False
      state: enabled

  forward_ports:
    - proto: "tcp"
      port: "50022"
      toaddr: "192.168.10.10"
      toport: "22"
      zone: public
      immediate: yes
      permanent: False
      state: enabled
```

## Variable parameters
### zones
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| zone | yes |  | string |  | zone name of target |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### targets
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| target | yes |  | string | default,<br />ACCEPT,<br /> %%REJECT%%<br />or<br />DROP  |  |
| zone | no |  | string |  | zone name of target |

### masquerades
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| masquerade | yes |  | string | yes<br />or<br />no  |  |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |

### interfaces
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| interface | yes |  | string |  | interface name of target |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### services
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| service | yes |  | string |  | service name of target |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### ports
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| port | yes |  | string |  | port of target |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### sources
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| source | yes |  | string |  | The target restricted connection source. |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### rich-rules
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| rule | yes |  | string |  | rich-rule value |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### icmp-blocks
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| type | yes |  | string |  | icmp block type |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |

### forward ports
| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| proto | yes |  | string |  | connection source protocol |
| port | yes |  | string |  | source port |
| toport | no |  | string |  | destination port |
| toaddr | no |  | string |  | destination address |
| zone | no |  | string |  | zone name of target |
| immediate | no | yes | string | yes<br />or<br />no | This configuration be applied immediately. |
| permanent | no | no | boolean | True<br />or<br />False | This configuration setting permanent. |
| state | yes |  | string | enabled<br />or<br />disabled | Add new zone if enabled. |


## Dependencies

None

## Example Playbook

```yaml
- hosts: servers
  roles:
     - { role: shhirose.firewalld }
  vars:
    shhirose_firewalld:
      services:
        - service: http
          zone: public
          immediate: yes
          permanent: True
          state: enabled
        - service: https
          zone: public
          immediate: yes
          permanent: True
          state: enabled
      ports:
        - port: 8080/tcp
          zone: public
          immediate: yes
          permanent: True
          state: enabled
```

## License

MIT
