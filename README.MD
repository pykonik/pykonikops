To successfully setup new python meetup website you need:
1. Fill in group_vars/secret.yml and group_vars/secret.yml.
2. In file hosts replace `#ip address` with ip of your server
3. `ansible-playbook -i deployment/hosts deployment/core.yml` - this command will prepare server
for deploying meetpy. This playbook is using remote root user and ssh public key to login to server and it:
    1. Creates deployer user which name is defined in group_vars/all.yml
    2. Copies your ssh key to deployer user's authorized_keys.
    3. Installs all necessary packages
4. `ansible-playbook -i deployment/hosts deployment/deploy.yml` - this command is actually deploying meetpy application
with nginx, gunicorn, postgresql and supervisor
