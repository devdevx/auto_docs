# Ansible

## Installation

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

## Commands

````
ansible
ansible-playbook
ansible-galaxy
ansible-inventory
ansible-vault

sudo apt install python-pip

````



## Use cases

### Provisioning

#### Cloud

For integration testing.

#### Virtual machine

Comonly used by Vagrant

### Task automating

#### System reboot

#### Disaster recovery

### Configuration management

#### Patching

Automating all OS updates.

#### Kubernetes

Instead of helm.

#### Switch

Mass switch configuration changes.

### Application deployment

### Continuous delivery

#### CI/CD pipeline

In your CI/CD tool, use a template where first step just calls out your Ansible playbook for the actual build and deployment.

### Security automation

### Orchestration

### Dynamic documentation

## Structure

````
inventories/
   production/
      hosts               # inventory file for production servers
      group_vars/
         group1           # here we assign variables to particular groups
         group2           # ""
      host_vars/
         hostname1        # if systems need specific variables, put them here
         hostname2        # ""

   staging/
      hosts               # inventory file for staging environment
      group_vars/
         group1           # here we assign variables to particular groups
         group2           # ""
      host_vars/
         stagehost1       # if systems need specific variables, put them here
         stagehost2       # ""

library/                  # if any custom modules, put them here (optional)
module_utils/             # if any custom module_utils to support modules, put them here (optional)
filter_plugins/           # if any custom filter plugins, put them here (optional)

site.yml                  # master playbook
webservers.yml            # playbook for webserver tier
dbservers.yml             # playbook for dbserver tier

roles/
    common/               # this hierarchy represents a "role"
        tasks/            #
            main.yml      #  <-- tasks file can include smaller files if warranted
        handlers/         #
            main.yml      #  <-- handlers file
        templates/        #  <-- files for use with the template resource
            ntp.conf.j2   #  <------- templates end in .j2
        files/            #
            bar.txt       #  <-- files for use with the copy resource
            foo.sh        #  <-- script files for use with the script resource
        vars/             #
            main.yml      #  <-- variables associated with this role
        defaults/         #
            main.yml      #  <-- default lower priority variables for this role
        meta/             #
            main.yml      #  <-- role dependencies
        library/          # roles can also include custom modules
        module_utils/     # roles can also include custom module_utils
        lookup_plugins/   # or other types of plugins, like lookup in this case

    webtier/              # same kind of structure as "common" was above, done for the webtier role
    monitoring/           # ""
    fooapp/               # ""
````



## Components

### Inventory

#### Static

Can be a INI or a yaml file. Uses IPs (125.125.125.125) and FQDNs (domain.com).

````ini
[group-1]
host1
host2

[group-2]
host2
host3

[group-3]
host2
host3

[group-1_2:children]
group-1
group-2

[group-all:children]
group-1_2
group-3
````

### Variables

Is a yaml file.

#### Role variables

Variables related to a specific role, for example packager required in a webserver.

````yaml
webserver_packages:
  - nginx
  - git
````

#### Group variables

Variables related to a group of hosts, for example the ssh key used for all servers in zone.

````yaml
ansible_ssh_private_key_file: ~/.ssh/zone-1.pem
````

#### Host variables

Variables related to a specific host, for example ssh related data.

````yaml
ansible_connection: ssh
ansible_user: user
ansible_password: password
ansible_host: 123.123.123.123
ansible_port: 33
````

### Roles

Represents a sarting point comon in a system. Has all the required data to create a non customized installation of something.

### Tasks

Order to perform something.

## Good practices

Keep your playbooks, roles, inventory, and variables files in git or another version control system.

With cloud providers and other systems that maintain canonical lists of your infrastructure, use dynamic inventory to retrieve those lists instead of manually updating static inventory files.

If you create groups named for the function of the nodes in the group, for example webservers or dbservers, your playbooks can target machines based on function.

You can keep your production environment separate from development, test, and staging environments by using separate inventory files or directories for each environment. This way you pick with -i what you are targeting.



You should encrypt sensitive or secret variables with Ansible Vault. However, encrypting the variable names as well as the variable values makes it hard to find the source of the values. You can keep the names of your variables accessible (by `grep`, for example) without exposing any secrets by adding a layer of indirection:

1. Create a `group_vars/` subdirectory named after the group.
2. Inside this subdirectory, create two files named `vars` and `vault`.
3. In the `vars` file, define all of the variables needed, including any sensitive ones.
4. Copy all of the sensitive variables over to the `vault` file and prefix these variables with `vault_`.
5. Adjust the variables in the `vars` file to point to the matching `vault_` variables using jinja2 syntax: `db_password: {{ vault_db_password }}`.
6. Encrypt the `vault` file to protect its contents.
7. Use the variable name from the `vars` file in your playbooks.

When running a playbook, Ansible finds the variables in the unencrypted file, which pulls the sensitive variable values from the encrypted file. There is no limit to the number of variable and vault files or their names.

## ansible-config

Used to detect changes between default config and project config.

````bash
ansible-config dump --only-changed
````

Example of modified config in `ansible.cfg`:

````ini
[defaults]
roles_path = roles
log_path = ./ansible.log
````

## ansible-galaxy

Used to create new roles and import external existing roles from central repository. By default we can import any role from *https://galaxy.ansible.com*

````bash
ansible-galaxy install robertdebock.nginx
ansible-galaxy list
cd roles
ansible-galaxy init demo
cd ..
ansible-galaxy list
````

## ansible-inventory

Used to manage the inventory.

````bash
ansible-inventory --list -i inventories/dev/hosts
````

## ansible-vault

Used to create and manage secure variable files (protected by password).

````bash
ansible-vault encrypt vault.yaml
ansible-playbook main.yaml -i inventories/dev/hosts --ask-vault-pass
ansible-vault view vault.yaml
ansible-vault edit vault.yaml
env EDITOR=nano ansible-vault edit vault.yaml
````

## ansible-playbook

````bash
ansible-playbook main.yaml -i inventories/dev/hosts
````



