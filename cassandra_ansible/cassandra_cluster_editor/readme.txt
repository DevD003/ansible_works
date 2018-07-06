~~~ install cassandra on individual nodes ~~~

> ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook cassandra.yml -i '<node-ip>,<node-ip>,' -e 'ansible_ssh_user=XXXXX ansible_ssh_pass=XXXXXX ansible_sudo_pass=XXXXXX'

~~~ configuring cassandra cluster ~~~

# nodes to be seeds and peers
# node-details (ansible_ssh_user=XXXXX ansible_ssh_pass=XXXXXX ansible_sudo_pass=XXXXXX) of each node to ./hosts-[seed_node],[peer_node]

> ansible-playbook cassandra_cluster_cfg.yml  
#creates and configures nodes to a cluster and starts cluster

~~~ add_node to existing cluster ~~~

# install cassandra on new_nodes
# node-details (ansible_ssh_user=XXXXX ansible_ssh_pass=XXXXXX ansible_sudo_pass=XXXXXX) of new_nodes to ./hosts-[add_nodes]...

> ansible-playbook cassandra_new_node_cfg.yml 
# adds node(s) to cluster && balance data replication

~~~ remove_node from existing cluster ~~~
# node-details (ansible_ssh_user=XXXXX ansible_ssh_pass=XXXXXX ansible_sudo_pass=XXXXXX) of removing_nodes to  > ./hosts-[remove_nodes]...

> ansible-playbook cassandra_remove_node.yml 
# decommissions node from cluster &&  uninstall cassandra

Notes:
 -> The name of the cluster can be specified at the [______ :children] at the top of ./hosts file. Name should be in Upper-case* 
 -> If Ansible to nodes are configured already, details can be skipped except fot the ip address.
 -> If node details are not specified, change {{ ansible_ssh_host }} to {{ inventory_hostname }} in roles/cassandra_cluster_cfg (or) new_node_cfg /Wait for Server Restarit/host:
 -> Multi-layer auth. usage when ANSIBLE_KEY_CHECKING=False may result in ---error--- at >> Wait for Server Restart << Comment out or manually reboot server to get around.
