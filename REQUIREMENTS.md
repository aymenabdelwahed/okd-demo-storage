# okd-demo-storage requirements

Requirements for this demo

You need to have the correct Red Hat Subscription allowing access to Red Hat Openshift Container Platform channels in order to install OCP.
You will need to provision one or several RHEL Servers depending on your needs for the Openshift cluster.
In our demo, there is only one server running an all-in-one Openshift cluster.
In AWS, a t2.xlarge or t2.2xlarge is sufficient for testing/POC needs.
The specifications for the servers and the steps to follow can be found in the Red Hat Document: https://access.redhat.com/documentation/en-us/openshift_container_platform/3.11/html/installing_clusters/

## Openshift installation

Once your servers are properly setup, you need to create your inventory file (/etc/ansible/hosts) that will be used in the playbook to install Openshift.
There are some examples in the Red Hat Documentation.
Here is the inventory used in the demo:
```yaml
[OSEv3:children]
masters
nodes
etcd

[OSEv3:vars]
ansible_ssh_user=root
os_firewall_use_firewalld=true
openshift_deployment_type=openshift-enterprise
#openshift_portal_net=172.30.0.0/16
## localhost likely doesn't meet the minimum requirements
openshift_disable_check=disk_availability,memory_availability

#Cluster Authentication Variables

openshift_master_identity_providers=[ {'name':'htpasswd_auth','login':'true','challenge':'true','kind':'HTPasswdPasswordIdentityProvider'} ]
openshift_master_htpasswd_users={'admin':'adminpasswd','developer':'developerpasswd'}

openshift_master_default_subdomain=cloudapps.example.com

oreg_url=registry.redhat.io/openshift3/ose-${component}:${version}
#Red Hat login
oreg_auth_user=
oreg_auth_password=

openshift_node_groups=[{'name': 'node-config-all-in-one', 'labels': ['node-role.kubernetes.io/master=true', 'node-role.kubernetes.io/infra=true', 'node-role.kubernetes.io/compute=true']}]

#Below, you can use IP, FQDN or localhost if you install and run the installer on the master server
[masters]
localhost ansible_connection=local

[etcd]
localhost ansible_connection=local

[nodes]
#openshift_node_group_name should refer to a dictionary with matching key of name in list openshift_node_groups.
localhost ansible_connection=local openshift_node_group_name="node-config-all-in-one" openshift_public_hostname=example.com openshift_public_ip=
```

## NFS server

Althought NFS doesn't offer the best performances, it is often used in order to provide persistent storage.
Create a dozen or more folders that will be presented to the cluster in /etc/exports.
For example:
```bash
	/PersistentStorage/sto1 *(rw,root_squash)
	/PersistentStorage/sto2 *(rw,root_squash)
	/PersistentStorage/sto3 *(rw,root_squash)
	/PersistentStorage/sto4 *(rw,root_squash)
	/PersistentStorage/sto5 *(rw,root_squash)
	/PersistentStorage/sto6 *(rw,root_squash)
	/PersistentStorage/sto7 *(rw,root_squash)
	/PersistentStorage/sto8 *(rw,root_squash)
	/PersistentStorage/sto9 *(rw,root_squash)
	/PersistentStorage/sto10 *(rw,root_squash)
```


## AWS Configuration

You will need to associate Elastic IPs to your servers and NFS server if you plan to shut them down from time to time. If not their public IP wil change when you start them back up and the servers won't be able to reach each other.
Also, if you use FQDN in the inventory or /etc/fstab you will need to create DNS entries in Route53 for the servers as well as a wildcard for the app url (when new routes will be created).
