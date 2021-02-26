![Data Machines Corp.](https://avatars2.githubusercontent.com/u/16696043?s=200)

# Ansible Role Docker PowerDns
> Deploy PowerDNS, recursor, admin UIs in Docker-compose
this ansible module will deploy all neccessary dependency to  store and manage  powerDNS, 
they consistsed of 
- powerdns authoritative server
- powerdns Recursor
- mysql database
- powerdns admin WSGI server
- powerdns admin Ui web server


## Installation
### install dependencies
* pip3 install -r requirments.txt


* Install complementary roles:
```bash
ansible-galaxy install -r install_roles.yml

For some version of ansible on MacOs, you might run into cert issue, simply 
ansible-galaxy --ignore-certs install -r install_roles.yml to install role files to ~/.ansible/role folder
```


* #### Setup environment variable for Hashcorp Vault lookup
  ##### note if don't want to use vault to store you password, you could skip this step, and simply change `lookup_vault` in group_var/all.yml to false


  Source the following environment to configure your environment for the connectivity information used by the 
`ansible-modules-hashivault` module to communicate with Vault.  
 ``````bash
#!/usr/bin/env bash  
# Hashicorp vault environment variables to access vault from the lookup plugin  
# .vault-token should be set to vault master token, https://vault_server/ui/vault/secrets/secret/show/vault-tokens  
export VAULT_TOKEN=$(cat ~/.vault-token)  
export VAULT_ADDR=https://$vault_server
export VAULT_SKIP_VERIFY=1  
``````

## Using the role
Now you are ready to run the playbook and deploy PowerDNS.  
```
ansible-playbook --private-key=key --user=ubuntu --extra-var "project_name=$projectGroup"  -v site.yml  
```

#### Notice: powerdns admin ui is available via http://$ip:8080
to create a admin user, click on "register" on webui. the first user register/created become a admin user. remember to turn off "Allow users to sign up" function in settings->authentication tab after initial registration. 


## Links

Even though this information can be found inside the project on machine-readable
format like in a .json file, it's good to include a summary of most useful
links to humans using your project. You can include links like:
- powdns: [https://www.powerdns.com/documentation.html]
- pdns-admin:  [https://hub.docker.com/r/pschiffe/pdns-admin-uwsgi]
- Repository: [https://github.com/datamachines/ansible-role-docker-pdns]
- Issue tracker: [https://github.com/datamachines/ansible-role-docker-ipa/issues]
  - In case of sensitive bugs like security vulnerabilities, please contact
    help@datamachines.io directly instead of using issue tracker. We value your effort
    to improve the security and privacy of this project!
- Related projects:
  - DataMachines: [https://datamachines.io]
  - Docker Hub Organization: [https://hub.docker.com/u/datamachines/]

## Contributing

If you'd like to contribute, please fork the repository and use a feature branch. Pull requests are warmly welcome. 

## Licensing

All rights reserved. 



