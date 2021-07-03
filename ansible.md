# Ansible Best Practices
The collection of best practices show that how to use the Ansible effectively

## 1. Directory Layout
This is the directory layout of this repository with explanation.

    ansible.cfg
    inventories/
        production/
            hosts.yml            # inventory file for production servers
            group_vars/
                group1.yml       # here we assign variables to particular groups
                group2.yml
            host_vars/
                hostname1.yml    # here we assign variables to particular systems
                hostname2.yml

        staging/
            hosts.yml            # inventory file for staging environment
            group_vars/
                group1.yml       # here we assign variables to particular groups
                group2.yml
            host_vars/
                stagehost1.yml   # here we assign variables to particular systems
                stagehost2.yml
    playbooks/
        deploy-webserver.yml
        deploy-application.yml

    library/
    module_utils/
    filter_plugins/

    roles/
        freeswitch/
        nginx/
        kamailio/
        asterisk/
        libresbc/


## Always Name Tasks
It is possible to leave off the ‘name’ for a given task, though it is recommended to provide a description about why something is being done instead. This name is shown when the playbook is run.

## Keep It Simple
When you can do something simply, do something simply. Do not reach to use every feature of Ansible together, all at once. Use what works for you. If something feels complicated, it probably is, and may be a good opportunity to simplify things.

## Version Control
Use version control. Keep your playbooks and inventory file in git (or another version control system), and commit when you make changes to them. This way you have an audit trail describing when and why you changed the rules that are automating your infrastructure.

## Group By Roles & Geography
Machines should be group based on role, as well as geography to assign specific variables using the group variable system.
## Encrypting Passwords and Certificates
It is most likely that you will have a password or certificates in your repository. It is not a good practice to put them in a repository as plain text. You can use ansible-vault to encrypt sensitive data. You can refer to password.yml in group variables to see the encrypted file and password-plain.yml to see the plain text file, commented out. To decrypt the file, you need the vault password, which you can place in your root directory but it MUST NOT be committed to your git repository. You should share the password with you coworkers with some other method than committing to git a repo.

There is also git-crypt that allow you to work with a key or GPG. Its more transparent on daily work than ansible-vault
