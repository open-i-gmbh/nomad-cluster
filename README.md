# README


## requirement

* Virsualbox https://www.virtualbox.org/wiki/Downloads
* vagrant https://www.vagrantup.com/downloads

## How to use the Repo:

* clone the repo

```
git clone https://github.com/mahmoud-mahdi/nomad_vm.git
```

* Provision the evviroment

```
vagrant up  #Build the vms

vagrant ssh [master1|node1|node2]  #to connect via ssh to any vm

ansible-playbook -i ./inventory playbook.yml   #to Provision the enviroment

## connect to the master node and check the nomad status as following:

nomad server members
nomad status
nomad node status
```


* deploy a test Job

```
cd /vagrant/
nomad run webapp.nomad  ### To submit the Job
nomad status demo-webapp  ### Check the Job status

nomad run nginx.nomad   ### Deploy nginx to use as loadbalancer 'reverse proxy'
nomad status nginx
nomad alloc fs 1eb nginx/local/load-balancer.conf  ### Check the registerd backend servers

curl nginx.service.consul:8080
```

### Connect to Nomad webui and consul webui and check the deployment status
* http://192.168.50.10:8500/ui/dc1/services
* http://192.168.50.10:4646/ui/jobs
