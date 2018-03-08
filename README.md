# ansibletask: Deploy a php file to two web servers

### Usage

`ansible-playbook -i production deploy-app.yml -e rel=v1`


### Notes

* The web hosts in this case are Ubuntu 16.04 and thus a ppa was not needed.
* The variable *rel* describes the version number which is a git tag in this case.
* The *app* role installs the site-specific config and enables php there.


## Second option for deployment

The deployment deploys to two webservers in parallel. This playbook coudl be change to deploy one by one using the serial option:
serial: 1 

If one had these webserver behind haproxy for example, one could first put the first server into maintenance mode in haproxy, and then deploy the code, prehaps have a unti test run, renable the server in haproxy, and then do this all again for the next server in the inventory file.


### Testing the playbook

To run these playbooks to make sure the work properly 

* apt-get install ansible
* Make two virtual machines
** `mkdir box1`
** `cd box1`
** `vagrant init ubuntu/xenial64´
** added `config.vm.network "forwarded_port", guest: 80, host: 8081` to Vagrantfile under config.vm.box
** `vagrant up`
** `vagrant ssh`
*** added my ssh public key to vagrant user authorized_keys
*** `sudo apt-get install python`
*** `exit`
** vagrant ssh-config (To get ssh port number and put that in my ansible inventory file)

After making the two boxes as above the playbook worked nicely.


