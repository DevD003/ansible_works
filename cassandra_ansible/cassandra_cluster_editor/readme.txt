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
