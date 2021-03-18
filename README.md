# Challenge-OutCloud
2 Ansible Playbooks for a Webserver and a Database server

This playbook will execute a initial server setup for Ubuntu 18.04 systems and install a Wordpress webserver and a MySQL server.
A number of containers will be created with the options specified in the `group_vars/wordpress/default.yml`, `group_vars/mysql/default.yml` variable files.

## Settings

- `create_user`: the name of the remote sudo user to create.
- `copy_local_key`: path to a local SSH public key that will be copied as authorized key for the new user. By default, it copies the key from the current system user running Ansible.
- `sys_packages`: array with list of packages that should be installed.
- `php_modules`:  An array containing PHP extensions that should be installed to support your WordPress setup. You don't need to change this variable, but you might want to include new extensions to the list if your specific setup requires it.
- `mysql_root_password`: The desired password for the **root** MySQL account.
- `mysql_db`: The name of the MySQL database that should be created for WordPress.
- `mysql_user`: The name of the MySQL user that should be created for WordPress.
- `mysql_password`: The password for the new MySQL user.
- `http_host`: Your domain name.
- `http_conf`: The name of the configuration file that will be created within Apache.
- `http_port`: HTTP port for this virtual host, where `80` is the default. 


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

#System Settings
php_modules: [ 'php-curl', 'php-gd', 'php-mbstring', 'php-xml', 'php-xmlrpc', 'php-soap', 'php-intl', 'php-zip' ]

#MySQL Settings
mysql_root_password: "passwordexample"
mysql_db: "databasename"
mysql_user: "usersql"
mysql_password: "usersqlpassword"

#HTTP Settings
http_host: "http_host"
http_conf: "http_host.conf"
http_port: "80"
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
