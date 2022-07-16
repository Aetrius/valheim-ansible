Ansible Managed Games [Valheim] - @Aetrius
=============

[Fully deployable valheim project]
```[OS: Ubuntu 22.04]```
```[2 vCPU]```
```[4GB RAM]```

#### Assumptions: 
#### 1.  user ```tadmin``` is created with a known password. 
#### 2.  Networking is valid between the control (ansible) plane to the host vm(s).
#### 2.1 If local allow port forwarding, otherwise, if using aws configure security groups to allow ports exposed to the web for 2456.
#### 3.  This was deployed via local VMs running Ubuntu.
#### 4.  Using a prior Game install you will overwrite the HAULN.db and HAULN.fwl files by cloning this repo, and replacing the files.
#### 5.  If you do not want to use plugins, delete the .dlls. Try some cool mods. Copy the .dll files and FOLLOW the
####      directions provided in the plugins directories.
#### 6.  Should a plugin be an issue, update the .dll files in the github repo.
#### 7.  Add an ssh folder to the project, and add your ssh keys for ansible.

# Ansible Tower / Ansible

## INSTALLATION
[Prep ansible from a Windows PC, Install WSL for Ubuntu]
1. Add an SSH key for the WSL instance
2. Copy the SSH key to the host to deploy ansible against
3. Configure hosts/inventory.yml to use the proper yaml syntax
4. Run the Setup.yml file against the host to configure the networking with Netplan
5. Run the docker.yml file with the command below and the proper target name from inventory
6. Replace ```games/HAULN.db``` && ```games/HAULN.fwl``` with your custom games. We use a few mods, so if you use these game files you likely will run into a potential issue.

## Configuration
1. If local (Allow Port Forwarding) || If (cloud/aws) (Allow security group ports to valid addresses)

## RUN
```ansible-playbook -i hosts/inventory.yml docker.yml -Kk --extra-vars "target=prox-aether01"```

On the host run the start.sh as sudo | root
```sudo ./sync.sh```
This will run a docker-compose in a detached state so you can still use the VM without breaking the docker run.
```sudo docker ps```  will give you the docker container name.
```sudo docker logs container-name``` - use the container name from the previous line to see the container logs.


Copy new plugins to the games/plugins directory. Run the docker.yml file command above to re-deploy any new files.

## TODO
#### Need to create a crontab function to start the service if it's not working
#### Add a new feature to record to slack
#### Create a slack integration for restarting the server

# Go Forth Yee Viking - Oden is calling
