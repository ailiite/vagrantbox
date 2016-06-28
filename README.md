## Centos Development Environment

## Prerequisites

In order to run the development environment locally you will need

* VirtualBox 4.3.14 or above (https://www.virtualbox.org/wiki/Downloads)
* Vagrant (http://www.vagrantup.com/downloads.html) Versions 1.65+
* git must be installed locally

### Configuring the hostfile

Before using the service ensure that the following line is in your hostfile on the host machine. (Normally in /etc/hosts)

```
172.16.10.10 vagrant.local
```

You will also want to add to the hosts file all the services expect.  
That entry should look like
```
172.16.10.10 vagrant.local webserver.local api.local someotherservice.local 
```

### Configuring SSH agent forwarding

To allow github repos to be cloned down while inside the vagrant box, you need to give it access to your local ssh keys. Create your ssh config file if you don't have one already:

```
touch ~/.ssh/config
```
and add the following lines:
```
Host 172.16.10.10
   ForwardAgent yes
```
If after 'vagrant up vagrantbox' you get the following error message -

```
"The SSH command responded with a non-zero exit status...."
```

Then enter the following on the mac -

```
ssh-add ~/.ssh/id_rsa
```


## Creating the environment

From the directory containing this repository run

```
vagrant up
```

This will create the virtual machine. Next, log into the virtual machine using the command:

```
vagrant ssh
```

This will log into the machine and check out all of the applications in the */vagrant/apps* directory.

## If your environment becomes corrupted


To clean out the whole environment and begin again from scratch you can run the following commands from the host machine, not inside the VM.

```
vagrant halt
vagrant destroy
vagrant up
```
