# RHOSD 2019 - Cosa puoi fare con ansible in 1200 secondi
Inside the repository is possibile to collect all the files used during the RedHat OpenSource Day 2019 in Rome and Milan about our speech "Cosa puoi fare con Ansible in 1200 secondi".
With our **init-ocp-host.yml** is possible to prepare your hosts for an OpenShift Container Platform 3.11 in order to start the prerequisite and deploy_cluster playbooks provided by the OKD Community.

Create an inventory file with your settings and nodes like this:

```
[OSEv3:children]
masters
nodes
etcd

[etcd]                                                                                                                       
master.your-domain.it
app01.your-domain.it
app02.your-domain.it

[masters]
master.your-domain.it openshift_node_group_name='node-config-master-infra' 

[apps]
app01.your-domain.it openshift_node_group_name='node-config-compute'
app02.your-domain.it openshift_node_group_name='node-config-compute'

[nodes]
master.your-domain.it openshift_node_group_name='node-config-master-infra' 
app01.your-domain.it openshift_node_group_name='node-config-compute'
app02.your-domain.it openshift_node_group_name='node-config-compute'

[OSEv3:vars]
ansible_ssh_user=root
openshift_deployment_type=origin
openshift_release=v3.11
....
```

Execute the playbook in this way:

```
ansible-playbook -i inventory init-ocp-host.yml
```

Enjoy it


