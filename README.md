# Kubernetes Cluster Bootstrap w/ Ansible
This Ansible plabyook creates a (1) master and (3) worker Kubernetes cluster on Ubuntu Server 18.04 LTS.

## PREREQUISITES
- Ubuntu Server 18.04 LTS w/ internet connectivity
- Ansible 2.9.X installed on host executing playbooks
- Configure DNS on servers and Ansible host beforehand

## CONFIGURATION
In ```inventory.ini``` set hostnames and the remote user for Ansible to target during execution. In addition, examples of custom variables that can be set to tailor your installation are:

- ```kcli_version=1.18.1-00```
- ```k8s_version=1.18.1```
- ```k8s_environment=bare-metal```
- ```cert_sans=["name", "name.domain.com"]```
- ```pod_network_calico=https://docs.projectcalico.org/v3.11/manifests/calico.yaml```

The ```kcli_version``` is the version of kubeadmn that is avaiable in the Ubuntu repoistory. It can be found by running ```sudo apt-cache policy kubeadm``` after repository is added. The ```k8s_environment``` can be set to either ```aws``` or ```bare-metal```. Set to ```aws``` when you want to leverage the AWS Cloud Provider during Ansible bootstrap.
    
## DEPLOYMENT
Run the following command on systems that REQUIRE a sudo password to escalate priviledges:

```ansible-playbook playbook.yaml -i inventory.ini -K```

Run the following command on systems that DO NOT REQUIRE a sudo password to escalate priviledges:

```ansible-playbook playbook.yaml -i inventory.ini```
