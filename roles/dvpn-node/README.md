# Ansible Role for Sentinel dVPN Node

This Ansible playbook automates the deployment and configuration of the Sentinel dVPN Node. 
It handles tasks such as:
- building the dVPN Node, 
- initiating its configuration, 
- generating the Node wallet, 
- setting up the service for the dVPN node.
In default configuration role deploys node configuration which creates node wallet keys in test keyring (means no password is required to start node).
This can be adjusted in configuration template.

## Prerequisites

- **Golang**: This playbook requires Golang to be deployed on the server. If you haven't already set up Golang, you can use the provided Ansible role named [`golang`](github.com/ChainTools-Tech/ansible-roles/tree/main/roles/golang) to do so.

## Role Variables

The `dvpn-node` role uses the following variables:

| Variable               | Default Value                         | Description                                           |
|------------------------|---------------------------------------|-------------------------------------------------------|
| `node_user`            | `"sentinel"`                          | User for the dVPN Node.                               |
| `node_group`           | `"sentinel"`                          | Group for the dVPN Node.                              |
| `node_repo`            | `"https://github.com/sentinel-official/dvpn-node"` | Repository URL for the dVPN Node.                     |
| `node_version`         | `"v0.7.0"`                            | Version of the dVPN Node to deploy.                   |
| `node_operator_key_pass` | `"password"`                        | Password for the Node operator wallet. (Used only when keyring backend is changed to file.)                   |
| `node_port`            | `"29843"`                             | Port for the dVPN Node.                               |
| `wireguard_port`       | `"12121"`                             | Port for the WireGuard.                               |
| `output_folder`        | `"/home/ubuntu/output/dvpn-node"`     | Folder to store the output related to the dVPN Node wallet details.  |

## Usage

1. Ensure Golang is set up on the server. If not, deploy it using the [`golang`](github.com/ChainTools-Tech/ansible-roles/tree/main/roles/golang) role.
2. Configure the variables as per your requirements.
3. Call the `dvpn-node` role in your playbook.

Example:

```yaml
- hosts: your_target_host
  roles:
    - dvpn-node
```

## Conclusion

This playbook simplifies the process of setting up and configuring the Sentinel dVPN Node. Ensure you have the necessary prerequisites in place and adjust the variables as needed before running the playbook.

## License
MIT

## Author Information
Questions and support: support@chaintools.tech
