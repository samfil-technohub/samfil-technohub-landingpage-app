## Documentation
Prerequisite
---
Install ansible, virtualbox, and vagrant on your local machine.

Running the Application
---
- Clone this repository.
- Create ssh key pair within the ~/.ssh directory with the name server_key
- Clone the configuration repository within the application parent directory `git clone https://github.com/samfil-technohub/samfil-technohub-landingpage-config.git configuration`
- Run `vagrant up --provision` to boot and configure the VM.

Viewing the Application
---
Application URL: 192.168.255.9