Role Name
=========

This role allows to configure an power dns services consisted of mysql database, powerdns auth server, powerdns-recursor/forwarder, powerdns admin ui


Requirements
------------
docker  
docker-compose  
Ansible version: 2.8+

Role Variables
--------------
### base variable:
#### see roles/pdns/defaults/main.yml for default values

#### Pdns environment variable
pdns_root_dir: /opt/pdns
MYSQL_USER: root  
MYSQL_PASS: changeme  
MYSQL_PORT: 3306  
pdns_docker_image:  psitrax/powerdns  
#local pdn configuration directory, whre pdns.conf should be copy to   
pdn_config_dir: /opt/pdns/config/pdns  
pdns_port: 54  
#assign a ip, so it can be references in pdns-recursor as  forwarder  
pdns_ip: 192.168.96.3  
PDNS_API_KEY: aiHoobeeghoo8eeCiwe2uQuah8eecoh5sdf  
PDNS_VERSION: 4.1.1   

#### pdns recursor environment variable  
pdns_recursor_config_file: /opt/pdns/config/pdns-recursor/  recursor.conf  
pdns_recursor_port: 53  
pdns_recursor_image: lmnetworks/pdns-recursor:latest  
pdns_recursor_ip: 192.168.96.4  

#### db   
db_image: mariadb:10.1  
db_data_dir: /opt/mysql-data  
db_ip: 192.168.96.2  

#### pdns admin ui variables  
pdns_admin_uwsgi_image: pschiffe/pdns-admin-uwsgi:ngoduykhanh  
pdns_admin_uwsgi_ip: 192.168.96.5  
pdns_admin_static_image: pschiffe/pdns-admin-static:ngoduykhanh  
pdns_admin_static_ip: 192.168.96.6  
pdns_admin_upload_dir: /opt/pdns-admin-upload  


##### network  
networks_subnet: 92.168.96.0/24  
networks_gateway: 192.168.96.1  




Dependencies
------------
ansible  
docker-compose


#### following playbook uses hashivault to store sensitive information. install ansible-modules-hashivault and environment prior running. (Note, if you choose to store sensitive data in local variable file,  you could set variable directoy in vars/main.yml and comment out part that does lookup)



pip install `ansible-modules-hashivault`

source following environment prior running ansible to look up vault 
#!/usr/bin/env bash
### Hashicorp vault environment variables to access vault from the lookup plugin
#### .vault-token should be set to vault master token, https://10.1.90.26:8200/ui/vault/secrets/secret/show/vault-tokens
```
export VAULT_TOKEN=$(cat ~/.vault-token)
export VAULT_ADDR=https://10.1.90.26:8200
export VAULT_SKIP_VERIFY=1

```

Example Playbook
----------------
```
- name: playbook to configure PowerDNS cluster in docker-compose   

  hosts: pdns
  become: yes
  
  vars:  
        MYSQL_PASS: "newMySqlPassword" 
        PDNS_API_KEY: "apikey for pdns" 
		
  roles:
  - role: pdns
  

```
License
-------

BSD

Author Information
------------------
Annie weng   
annieweng@datamachines.io  
Data Machine Corps

