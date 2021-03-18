# Challenge-OutCloud
2 Ansible Playbooks for a Webserver and a Database server

This playbook will execute a initial server setup for Ubuntu 18.04 systems and install a Wordpress webserver and a MySQL server.
A number of containers will be created with the options specified in the `group_vars/wordpress/default.yml`, `group_vars/mysql/default.yml` variable files.

## Settings

- `create_user`: the name of the remote sudo user to create.
- `copy_local_key`: path to a local SSH public key that will be copied as authorized key for the new user. By default, it copies the key from the current system user running Ansible.
- `sys_packages`: array with list of packages that should be installed.


## Running the Playbooks

Quick Steps:

### 1. Obtain the playbooks
```shell
git clone https://github.com/gonribago/Challenge-OutCloud.git
cd ansible-playbooks/setup_ubuntu1804
```

### 2. Customize Options

```shell
nano group_vars/wordpress/default.yml
nano group_vars/mysql/default.yml
```

```yml
#group_vars/wordpress/default.yml
#group_vars/mysql/default.yml
---
create_user: adm
copy_local_key: "{{ lookup('file', lookup('env','HOME') + '/.ssh/id_rsa.pub') }}"
sys_packages: [ 'curl', 'vim', 'git', 'ufw']

mysql_root_password: "passwordexample"
mysql_db: "databasename"
mysql_user: "usersql"
mysql_password: "usersqlpassword"
```

### 3. Run the Playbooks

### Run the Wordpress Playbook
```command
ansible-playbook playbook_wordpress.yml -kK
```

### Run the MySQL Playbook
```command
ansible-playbook playbook_mysql.yml -kK
```
