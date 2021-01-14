Clone Private Git Repository
=========
An Ansible role that can be used to clone a private GitHub repository. 


Requirements
------------
* This role requires a GitHub personal access token. Generate a new token (Settings -> Developer Settings -> Personal Acess Token). Make sure the token has the scopes outlined in the "Role Variables" section below.

* Create a password file that will be used to encrypt the GitHub personal access token

    `echo "<your-passphrase>" | openssl aes-256-cbc -a -salt > /path/to/password/file`

* In order to let Ansible know where to look for the password file, you have two options:

  1. In the `ansible.cfg` file, add the line: `vault_password_file = /path/to/password/file` under [defaults]

  2. Create an environment variable: `ANSIBLE_VAULT_PASSWORD_FILE=/path/to/password/file`

* Encrypt the token by running the following command
    
    `ansible-vault encrypt_string '<token>' --name 'GITHUB_ACCESS_TOKEN' --vault-password-file=/path/to/password/file`

* Copy the generated encrypted string and paste it in the vars/main.yml file

Role Variables
--------------

* KEY_TITLE: The title of the SSH key to be added to the GitHub account
* KEY_PATH: Full path of the directory where the SSH key should be stored. A typical location would be `~/.ssh/<key_name>`
* GITHUB_ACCESS_TOKEN: The personal access token associated with the GitHub account being used. The token should have the following scopes: 
  - repo
  - admin:public_key
  - user
  - admin:gpg_ley
* GIT_REPO: The SSH url of the GitHub repository to be cloned. An example would be `ssh://git@github.ibm.com/IBMZSoftware/nazare-demo-imsapp.git`
* CLONE_DEST: The folder where repository should be cloned to
* KNOWN_HOSTS_PATH: Location of the SSH `known_hosts` file on the target machine. A typical location would be `~/.ssh/known_hosts`
* GIT_EXECUTABLE: The location of the git binary on the target machine. For example `/usr/bin/git`


Example Playbook
----------------
    - hosts: servers
      roles:
         - git-clone

License
-------

BSD

Author Information
------------------

Author: Asif Mahmud

Email: asif@mahmudasif.com
