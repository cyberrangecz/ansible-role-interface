# Ansible role - Interface

This role serves for network interface configuration on debian-based systems.

## Requirements

* This role requires root access, so you either need to specify `become` directive as a global or while invoking the role.

    ```yml
    become: yes
    ```

* Also requires Ansible variables, therefore do not disable directive `gather_facts`.

## Role paramaters

Mandatory parameters.

* `interface_interfaces` - The list of network interface parameters. Each interface may consists of following attributes.
    * `interface_mac` (mandatory) - The MAC address of interface to configure.
    * `interface_default_gateway` (optional) - The IPv4 address of default gateway.
    * `interface_routes` (optional) - The list of route parameters. Each route must consist of following attributes.
        * `gateway` (mandatory) - The IPv4 address of default gateway for this route.
        * `network` (mandatory) - The IP address of network from which pakets will be routed.
        * `mask` (mandatory) - The subnet mask in address format or prefix number.

Optional parameters.

* `interface_clean` - Boolean value (**True**/**False**) that means whether to clean all interface configuration before applying role or not (default: True).
* `interface_mtu` - The number of maximum transmission unit (default: 1442).
* `interface_file_name` - The file name for your configuration located in `/etc/network/interfaces.d/` directory (by default the file `/etc/network/interface` is used).

## Example

Example of the simplest network interface configuration that just sets MTU of the specified interface.

```yml
roles:
    - role: interface
      interface_interfaces:
          - interface_mac: 01:23:45:67:89:ab
            interface_mtu: 1442
```
