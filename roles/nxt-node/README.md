ardor-node
==========

Role deploys most recent version of Ardor node and chain snapshot.
Deployment consists:
 - Required packages installation
 - Dedicated user creation
 - Configuration files upload and customization
 - Service deployment
 - Firewall setup

Supported platforms
-------------------
- Debian
- Ubuntu

Role was prepared and tested on Ubuntu 22.04 LTS

Role Variables
--------------
```yaml
ssh_port: "22"                                                           # SSH port used in firewall configuration
packages_list:                                                           # Required packages installed during deployment
  - pwgen
  - openjdk-11-jre-headless
  - default-jdk
client_bin_url: "https://www.jelurida.com/nxt-client.zip"                # URL pointing to client binaries archive
client_bin_archive: "nxt-client.zip"                                     # Name of client binaries archive file
chain_db_url: "https://www.jelurida.com/NXT-nxt_db.zip"                  # URL pointing to chain database snapshot
chain_db_archive: "NXT-nxt_db.zip"                                       # Name of chain snapshot archive file
node_download_folder: "/tmp"                                             # Folder where archives will be downloaded
node_user: "nxt"                                                         # Name of user which will run chain node
node_group: "nxt"                                                        # Name of group which will run chain node
node_home: "/home/nxt"                                                   # Home folder for node user
node_db_home: "{{ node_home }}/nxt"                                      # Location of chain database files
node_config_file: "nxt.properties"                                       # Node config file name
node_config_folder: "{{ node_db_home }}/conf"                            # Location of chain config file
node_service_name: "nxt"                                                 # Node service name
node_service_file: "/etc/systemd/system/{{ node_service_name }}.service" # Node service file location
ardor_my_platform: "UNDEFINED"                                           # Node specific platform ID; use host_vars to customize deployment
firewall_policies:                                                       # Default firewall policies
    - { direction: 'incoming', policy: 'deny' }
    - { direction: 'outgoing', policy: 'allow' }
firewall_rules:                                                          # Default firewall rules to allow node communication
    - { rule: 'limit', port: '{{ ssh_port | default("22") }}', proto: 'tcp', comment: "Secure Shell Access" }
    - { rule: 'allow', port: '7874', proto: 'tcp', comment: "NXT Node Peer Port" }
    - { rule: 'allow', port: '7876', proto: 'tcp', comment: "NXT Node API Port" }
```

variable for **host_vars**
```yaml
public_ip: "XXX.XXX.XXX.XXX"                                             # public IP of the server where node is installed
```
should be used when server has different IP than the one assigned to network interface. That variable shoul dbe placed specifically in ***host_vars*** for specific host prior to deployment, so configuration file can be adjusted accordingly. In case not specified IP address will be pulled from Ansible facts.


Dependencies
------------

No dependencies.

Example Playbook
----------------

**Playbook file: nxt.yml**
```yaml
---
- hosts: nxt
  gather_facts: True
  become: True
  roles:
    - nxt-node
```

**Inventory file: hosts**
```
[nxt]
node1.domain.com
node2.domain.com
```

**Playbook execution**
```bash
ansible-playbook nxt.yml -i hosts
```

License
-------

BSD

Author Information
------------------

Questions and support: support@chaintools.tech
