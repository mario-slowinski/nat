nat
===

Ansible role to configure NAT between public and internal network interfaces.

By default it translates traffic between:

* *public* interface, in *public* firewalld zone, with ip address = `ansible_host` variable
* *internal* interface, in *internal* firewalld zone, with ip address = `internal_ip` variable

Requirements
------------

* [ansible.builtin](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html)
* [ansible.posix](https://docs.ansible.com/ansible/latest/collections/ansible/posix/index.html)
* `nmcli` - NetworkManager CLI

Role Variables
--------------

* defaults

  ```yaml
  nat_interfaces: []      # list of network interfaces for NAT traffic
    - zone: ""            # name of firewalld zone
      interface: ""       # name of network interface
  ```

Dependencies
------------

No ansible roles dependencies

Tags
----

* **nat.firewall** - Configure firewall
  * **nat.firewall.zone** - Move interface to zone
  * **nat.firewall.masquerade** - Allow masquerade on public interface
* **nat.routing** - Configure ip forwarding
  * **nat.routing.forwarding** - Allow ip forwarding
  * **nat.routing.internal** - Disable default routing for non-public interfaces

Examples
--------

* `requirements.yaml`

  ```yaml
  - name: nat
    src: https://github.com/mario-slowinski/nat
  ```

* `playbook.yaml`

  ```yaml
  - hosts: servers
    gather_facts: true
    roles:
      - role: nat
  ```

License
-------

[GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.html)

Author Information
------------------

[mario.slowinski@gmail.com](mailto:mario.slowinski@gmail.com)
