UFW firewall configuring
=========

Configuring your UFW firewall

Role Variables
--------------

This is example for group vars:

```yaml
---
# defaults file for ufw
reset_old_rules: false

allow_networks:
  - net: "127.0.0.1/8"
    description: "loop"
  - net: 10.0.0.0/8
    description: "Private network"
  - net: 172.16.0.0/12
    description: "Private network"
  - net: 192.168.0.0/16
    description: "Private network"
  - net: "1.1.1.1"
    description: "Monitoring "

# Allow all firewall access from group hosts on everyone's nodes
allow_group_hosts: "{{ groups[group_names | last] | map('extract', hostvars, 'ansible_host') | list  }}"  #inventory_hostname

public_ports:
  - port: 22
    protocol: tcp
    description: "SSH"
  - port: 80
    protocol: tcp
    description: "HTTP"
  - port: 443
    protocol: tcp
    description: "HTTPS"
```


Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: ansible-role-ufw }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
