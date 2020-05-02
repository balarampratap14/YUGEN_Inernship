ansible-nagios
==============
Playbook for setting up the Nagios monitoring server and clients (CentOS)

# NAGIOS


## What does it do?
-------
   - Automated deployment of Nagios Server on CentOS7 or RHEL7
   - Automated deployment of Nagios client on CentOS6/7/8, RHEL6,7,8, Fedora and FreeBSD
     * Generates service checks and monitored hosts from Ansible inventory
     * Generates comprehensive checks for the Nagios server itself
     * Generates comprehensive checks for all hosts/services via NRPE
     * Generates most of the other configs based on jinja2 templates
     * Wraps Nagios in SSL via Apache
     * Sets up proper firewall rules (firewalld or iptables-services)
     * This is also available via [Ansible Galaxy](https://galaxy.ansible.com/sadsfae/ansible-nagios/)

## How do I use it?
-------
   - Add your nagios server under `[nagios]` in `hosts` inventory
   - Add respective services/hosts under their inventory group, **hosts can only belong under one group.**
   - Take a look at `install/group_vars/all.yml` to change anything like email address, nagios user, guest user etc.
   - Run the playbook.  Read below for more details if needed.

## Requirements
-------
   - RHEL7 or CentOS7 for Nagios server only.
   - RHEL6/7/8, CentOS6/7/8, Fedora or FreeBSD for the NRPE Nagios client
   - If you require SuperMicro server monitoring via IPMI (optional) then do the following
     - Install```perl-IPC-Run``` and ```perl-IO-Tty``` RPMs for RHEL7.
       - I've placed them [here](https://funcamp.net/w/rpm/el7/) if you can't find them, CentOS7 has them however.
     - Modify ```install/group_vars/all.yml``` to include ```supermicro_enable_checks: true```.
     
## Role Variables
-------
    ## for local caching of downloaded data

    local_cache_dir: "{{nagios_dir}}/cache"
        - nagios_email_address: "500061550@stu.upes.ac.in"

    ## nagios configurations
        - nagios_version: "4.4.5"
        - nagios_tgz_filename: "nagios-{{ nagios_version }}.tar.gz"
        - nagios_dir: /opt/nagios
        - nagios_core_dir: "{{nagios_dir}}/nagios-{{nagios_version}}"
        - nagios_base_dir: /usr/local/nagios
        - nagios_admin_user: nagiosadmin
        - nagios_admin_pass: nagiosadmin

    ## plugin configurations
        - nagios_plugins_version: "2.2.1"
        - nagios_plugins_tgz_filename: "nagios-plugins-{{ nagios_plugins_version }}.tar.gz"

All the above mentioned variables can be updated in inventory/group_vars/all.yml by providing in variable: value format.

## Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

## License
-------

BSD

## Files
-------
```
.
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
|   ├── create_nagios_common.yml
│   ├── enable_services.yml
│   ├── firewall.yml
│   ├── install_nagios_core.yml
│   ├── install_nagios_dependencies.yml
│   ├── install_nagios_plugin.yml
│   ├── main.yml
│   └── output_check.yml
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml

```
