## Documentation
Prerequisite
---
Install ansible, virtualbox, and vagrant within your local machine.

Running the Application
---
- create ssh key pair within the ~/.ssh directory with the name server_key
- eval `ssh-agent`
- ssh-add ~/.ssh/server_key
- clone the configuration repository within the application parent directory `git clone https://github.com/samfil-technohub/samfil-technohub-landingpage-config.git configuration`
- change into the directory and run `vagrant up` to boot the VM.

Viewing the Application
---.

Application URL: 192.168.255.9