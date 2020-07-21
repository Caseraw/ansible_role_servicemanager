# Ansible role service manager

Managing services.

[![Build Status](https://travis-ci.org/Caseraw/ansible_role_servicemanager.svg?branch=master)](https://travis-ci.org/Caseraw/ansible_role_servicemanager) [<img src="https://img.shields.io/ansible/role/49806">](https://galaxy.ansible.com/caseraw/ansible_role_servicemanager) [<img src="https://img.shields.io/ansible/role/d/49806">](https://galaxy.ansible.com/caseraw/ansible_role_servicemanager) [<img src="https://img.shields.io/ansible/quality/49806">](https://galaxy.ansible.com/caseraw/ansible_role_servicemanager)

- [Ansible role service manager](#ansible-role-service-manager)
  - [License](#license)
  - [Author Information](#author-information)
  - [Requirements](#requirements)
  - [Dependencies](#dependencies)
  - [Compatibility](#compatibility)
  - [Role Variables](#role-variables)
  - [Example Playbook](#example-playbook)
  - [Useful shell commands](#useful-shell-commands)
  - [Additional documentation resources](#additional-documentation-resources)
  - [Testing with Molecule](#testing-with-molecule)
  - [CI/CD with Travis CI](#cicd-with-travis-ci)
  - [Useful links](#useful-links)

## License

MIT / BSD

## Author Information

- Made and maintained by: [Kasra Amirsarvari](https://www.linkedin.com/in/caseraw)
- Ansible Galaxy community author: <https://galaxy.ansible.com/caseraw>
- Dockerhub community user: <https://hub.docker.com/u/caseraw>

## Requirements

- Ensure a package manager is available and configured with the correct package sources and repositories.
- Ensure systemd is running.
- Ensure privileged permissions are set for the user executing this role to:
  - Install packages.
  - Manage service settings and configurations.

## Dependencies

N/A

## Compatibility

Compatible with the following list of operating systems:

- CentOS 7
- CentOS 8
- RHEL 7.x
- RHEL 8.x

## Role Variables

| Variable name | Description |
|---------------|-------------|
| role_servicemanager_required_package_list | A list containing service details. |
| role_servicemanager_required_package_list.state | (required) Whether to manage the service; options: [present, absent]. |
| role_servicemanager_required_package_list.service_name | (required) The name of the systemd service. |
| role_servicemanager_required_package_list.service_state | (required) Which state to put the service in. |
| role_servicemanager_required_package_list.service_enabled | (required) Whether to enable or disable the service. |
| role_servicemanager_required_package_list.service_masked | (optional) Whether to mask or unmask the service. |
| role_servicemanager_required_package_list.systemd_daemon_reexec | (optional) Whether to serialize systemd state. |
| role_servicemanager_required_package_list.systemd_daemon_reload | (optional) Whether to reload systemd daemon. |
| role_servicemanager_required_package_list.systemd_force | (optional) Whether to force override existing symlinks. |
| role_servicemanager_required_package_list.systemd_no_block | (optional) Whether to enqueue job asynchronously. |
| role_servicemanager_required_package_list.systemd_scope | (optional) Whether to run systemctl within a given scope. |
| role_servicemanager_required_package_list.packages | (optional) A list of packages to install for the service. |

## Example Playbook

```yaml
---
- name: Manage services
  become: True
  gather_facts: True
  tasks:
    - import_role:
        name: ansible_role_servicemanager
      vars:
        role_servicemanager_service_list:
          - name: Process accounting
            state: present
            service_name: psacct
            service_state: started
            service_enabled: True
            service_masked: False
            packages:
              - psacct

...
```

## Useful shell commands

N/A

## Additional documentation resources

- <https://access.redhat.com/solutions/284403>
- <https://www.server-world.info/en/note?os=CentOS_7&p=psacct>
- <https://www.thegeekdiary.com/linux-os-service-psacct/>
- <https://www.tecmint.com/how-to-monitor-user-activity-with-psacct-or-acct-tools/>

## Testing with Molecule

This role is locally tested with the use of [Molecule](https://molecule.readthedocs.io/en/latest/), the configuration is located at: [molecule/default](molecule/default).  
The Molecule tests are run (using the [docker driver](https://molecule.readthedocs.io/en/latest/configuration.html#docker)) on [Dockerhub images](https://hub.docker.com/u/caseraw) built for this purpose:

- [CentOS](https://hub.docker.com/r/caseraw/ansible-molecule-centos)
- [Fedora](https://hub.docker.com/r/caseraw/ansible-molecule-fedora)

## CI/CD with Travis CI

This role uses [Travis CI](https://travis-ci.org/) to run online tests with the use of [Molecule](https://molecule.readthedocs.io/en/latest/) and pushes notifications to import the role into [Ansible Galaxy](https://galaxy.ansible.com/) once the tests are successful. The Travis CI configuration is located at the root of the Ansible role [.travis.yml](.travis.yml)

## Useful links

- GitHub repository: <https://github.com/Caseraw/ansible_role_arpwatch>
- Travis CI build status: <https://travis-ci.org/Caseraw/ansible_role_arpwatch>
- Ansible Galaxy role: <https://galaxy.ansible.com/caseraw/ansible_role_arpwatch>
