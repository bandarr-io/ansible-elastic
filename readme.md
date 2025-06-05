# Ansible Elastic Stack (from Connor)
To prepare for deployment:
1. Edit inventory.yml to update node names/IP addresses
    ```
      hosts:
        host1.my.tld: <- This can be a hostname **or** IP address
          ansible_host: 192.168.1.1
    ```
1. Edit group_vars/all.yml
    1. Update `esVersion` to reflect desired version number for the Stack
    1. Update passwords
1.  Edit my-cluster-elasticsearch_cluster.yml
    1. Please note, this naming convention allows you to support multiple clusters with a single playbook if needed. You can set `<some name>_elasticsearch_cluster.yml` to differentiate between cluster, along with a 2nd (or 3rd) inventory.yml file that reflects the cluster name.
    1. Change any combination of node names and roles as desired. The default config will create a 3 node cluster with all nodes having all roles.
1. Run `ansible-playbook -i inventory.yml -t prepare_hosts` first to generate certificates and configure the base OS itself
1. If deploying Fleet:
   1. Download Elastic Agent for your version of the Stack
   1. Place the `elastic-agent-<version>.tar.gz` file in the `packages` directory
1. Run `ansible-playbook -i inventory.yml` to deploy all configured node types  
