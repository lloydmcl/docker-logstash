## Logstash
### Description
This role is designed to install logstash on VMs running docker to be used in conjunction with docker-elasticsearch role.

### Warnings
Certificates served in the elk stack must be named according to the host they're being deployed to.

### Testing
This role was tested on the below versions
- Ubuntu 20.04
- Docker Version 20.10.5
- Elasticsearch 7.12
- Logstash 7.12

### Handlers
Handlers are used in this role and are documented below;

- **Restart logstash container**  
The intended use of this handler is to restart the logstash container when a config file has been updated.  

```
- name: Restart logstash container
  docker_container:
    name: "{{ logstash_hostname }}"
    restart: true
```

### Variables
Below are the variables used by this role;  

- **docker_network_name**  
The name of the docker network that will be associated with your logstash containers.

- **logstash_conf_dir**
Local persistent directory for Logstash config file.

- **logstash_certs_dir**
Local persistent directory on VM which will store certificates used for SSL.

- **logstash_hostname**
The name of your container.

- **logstash_image**
The image and version of Logstash you want to deploy.

- **docker_log_max_size**
The maximum json file size before the log is rolled.

- **docker_log_max_file**
The maximum number of log files that can be present.

- **logstash_log_level**
The level of verbosity you want Logstash to log. (eg. warn, info, debug)

- **logstash_username**
The logstash username to connect to the elasticsearch hosts with.

- **logstash_password**
The logstash password to connect to the elasticsearch hosts with.

- **groups['elastic_cluster_hosts']**
This is a required host group consisting of the elasticsearch cluster to connect Logstash to.

- **kibana_server_port**
The port to serve Kibana on.

- **kibana_server_host**
The IP address to which the Kibana server will bind.

- **groups['elastic_cluster_hosts']**
This is a required host group consisting of the elasticsearch cluster to connect Logstash to.

### Tags
- logstash
This tag will target all tasks related to this role.

### Additional Resources
https://docs.docker.com/config/containers/logging/local/
https://docs.ansible.com/ansible/latest/collections/community/docker/docker_network_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html
https://docs.ansible.com/ansible/latest/collections/community/docker/docker_container_module.html