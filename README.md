# Kubernetes Cluster Creator 
This Ansible plabyook creates a (1) master and (3) worker Kubernetes cluster on Ubuntu Server 18.04+.

## Prerequisites
- Ubuntu Server 18.04 LTS w/ internet connectivity

- Configure DNS on servers and Ansible host beforehand

## Configuration
* Set your Ansible master and workers in thte ```inventory.ini```. Tested with up to 3 workers.
* Set the following variables in ```inventory.ini```. Examples are the following:

    * ```kcli_version=1.18.1-00```
    
    * ```k8s_version=1.18.1```
    
    * ```k8s_environment=bare-metal```

    * ```cert_sans=["name", "fqdn"]```

    * ```pod_network_calico=https://docs.projectcalico.org/v3.11/manifests/calico.yaml```

* Notes: The ```kcli_version``` is the version of kubeadmn that is avaiable in the Ubuntu repoistory. It can be found by running ```sudo apt-cache policy kubeadm``` after repo is added. The ```k8s_environment``` can be set to either ```aws``` or ```bare-metal```. Set to ```aws``` when you want to leverage the AWS Cloud Provider.
    
## Deployment
Run the following command on systems that REQUIRE a sudo password to escalate priviledges:

```ansible-playbook playbook.yaml -i inventory.txt -K```

Run the following command on systems that DO NOT REQUIRE a sudo password to escalate priviledges:

```ansible-playbook playbook.yaml -i inventory.txt```
