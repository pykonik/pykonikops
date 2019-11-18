# Ansible provisioning and deployment for [meetpy](https://github.com/meetpy/meetpy)
To successfully setup new python meetup website you need:
1. Create your own secrets by cloning secret-example.yml. Eventually you can add vars which you want to override
from all.yml file.
2. In file `hosts` in new line add your server ip address.
3. `ansible-playbook -i hosts core.yml -limit <ip_address_of_your_server>` - this command will prepare server
for deploying meetpy. This playbook is using remote root user and ssh public key to login to server and it:
    1. Creates deployer user which name is defined in group_vars/all.yml
    2. Copies your ssh key to deployer user's authorized_keys.
    3. Installs all necessary packages
4. `ansible-playbook -i hosts deploy.yml  --extra-vars "@group_vars/secret-<your_meetup_name>.yml" -limit <ip_address_of_your_server>`
 - this command is actually deploying meetpy application
with nginx, gunicorn, postgresql and supervisor.
