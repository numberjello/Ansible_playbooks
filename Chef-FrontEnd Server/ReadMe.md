### Chef Cluster Playbooks


**Prequiste** 

You must have Python Library Ansible tool installed (brew install ansible and brew install python).

Wiki for these Playbooks for Chef Back-End and Front-End Servers


**Variables**

Adding New Chef Front End playbook: chef-fe.yml

Chef Cluster Key for new Chef Front end Nodes
Chef cluster key : private-chef-secrets.json.
The json file has been vaulted. 

Run --vault-password-file vaultpass.txt
Vault password: vaultpass.txt


***Running the Ansible-playbook for adding new Chef Front-end Server***

Update the inventory with the new server hostname target.

ansible-playbook -i inventory chef-fe.yml --vault-password-file vaultpass.txt --ask-become-pass -vvv





