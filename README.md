# Nutanix Role to deploy Prism Central

This Ansible role downloads and deploys Nutanix Prism Central.

## Requirements

The following roles need to be installed as they are used within this role;
- grdavies.nutanix_role_prism_initial_password
- grdavies.nutanix_role_prism_eula
- grdavies.nutanix_role_prism_pulse
- grdavies.nutanix_role_prism_container_search

```
ansible-galaxy install grdavies.nutanix_role_prism_init_api --force
ansible-galaxy install grdavies.nutanix_role_prism_initial_password --force
ansible-galaxy install grdavies.nutanix_role_prism_eula --force
ansible-galaxy install grdavies.nutanix_role_prism_pulse --force
ansible-galaxy install grdavies.nutanix_role_prism_container_search --force
```

## Role Variables

| Variable                                    | Required | Default         | Choices                                                                         | Comments                                                                                                                                                                                                                          |
|---------------------------------------------|----------|-----------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| validate_certs                              | no       | no              |                                                                                 | Whether to check if Prism UI certificates are valid.                                                                                                                                                                              |
| nutanix_pc_deploy_vm_name                   | no       | 'prism-central' |                                                                                 | The name of the Prism Central VM                                                                                                                                                                                                  |
| nutanix_pc_deploy_size                      | no       | small           | ['small', 'large', 'x-large']                                                   | See https://portal.nutanix.com/page/documents/details?targetId=Release-Notes-Prism-Central-vpc_2022_6:top-pc-scalability-r.html for details on PC sizing.                                                                         |
| nutanix_pc_deploy_container_name            | yes      |                 |                                                                                 | The name of the container (datastore) upon with to place the PC VM                                                                                                                                                                |
| nutanix_pc_deploy_subnet_name               | yes      |                 |                                                                                 | The name of the subnet (port-group) upon with to place the PC VM                                                                                                                                                                  |
| nutanix_pc_deploy_network_address           | yes      |                 |                                                                                 | Network address for the above subnet using the following notation (10.10.10.0/24)                                                                                                                                                 |
| nutanix_pc_deploy_gateway                   | yes      |                 |                                                                                 | IPv4 gateway  for the above subnet                                                                                                                                                                                                |
| nutanix_pc_deploy_ip_address                | yes      |                 |                                                                                 | IPv4 address for the above subnet to assign to the PC VM                                                                                                                                                                          |
| nutanix_pc_deploy_dns_list                  | no       | []              |                                                                                 | List of DNS servers ['8.8.8.8', '8.8.4.4']                                                                                                                                                                                        |
| nutanix_pc_deploy_version                   | no       |                 |                                                                                 | If not provided the latests Prism Central version for the clusters AOS version will be deployed.                                                                                                                                  |
| nutanix_pc_deploy_pulse                     | no       | True            | True | False                                                                    |                                                                                                                                                                                                                                   |
| nutanix_pc_deploy_eula_accept               | no       | False           | True | False                                                                    | If ELUA is set to True the full_name, company and role variables are mandatory.                                                                                                                                                                                                                                  |
| nutanix_pc_deploy_eula_full_name            | no       |                 |                                                                                 |                                                                                                                                                                                                                                   |
| nutanix_pc_deploy_eula_company_name         | no       |                 |                                                                                 |                                                                                                                                                                                                                                   |
| nutanix_pc_deploy_eula_job_title            | no       |                 |                                                                                 |                                                                                                                                                                                                                                   |


## Dependencies

- grdavies.nutanix_role_prism_init_api
- grdavies.nutanix_role_prism_initial_password
- grdavies.nutanix_role_prism_eula
- grdavies.nutanix_role_prism_pulse
- grdavies.nutanix_role_prism_container_search


## Example Playbook

```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.nutanix_role_prism_central_deploy
  vars:
    nutanix_host: 10.38.185.37
    nutanix_username: admin
    nutanix_password: nx2Tech165!
    nutanix_pc_deploy_container_name: Default
    nutanix_pc_deploy_subnet_name: Primary
    nutanix_pc_deploy_network_address: 10.38.185.0/25
    nutanix_pc_deploy_gateway: 10.38.185.1
    nutanix_pc_deploy_ip_address: 10.38.185.39
    nutanix_pc_deploy_dns_list:
      - 8.8.8.8
      - 8.8.4.4
    nutanix_pc_deploy_new_password: nx2Tech165!
    nutanix_pc_deploy_default_eula_accept: True
    nutanix_pc_deploy_default_eula_full_name: Ross Davies
    nutanix_pc_deploy_default_eula_company_name: Nutanix
    nutanix_pc_deploy_default_eula_job_title: SE
```


## License

See LICENSE.md

## Author Information

Ross Davies
