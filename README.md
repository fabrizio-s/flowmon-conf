(Configurations tested working with docker 26.0.1 and docker-compose version 2.26.1)

docker-compose.yml that will set up Elastiflow, Elasticsearch and Kibana for monitoring network traffic. Netflow must be configured from the router to send data to Elastiflow AFTER all three containers are up and running. Make sure all firewall rules are configured so as to allow this traffic. If you want to check whether Elastiflow is correctly receiving data from the router, change the following environment variables in flow-collector.env (https://docs.elastiflow.com/docs/config_ref/common/output_monitor#ef_output_monitor_enable):
    
    EF_OUTPUT_MONITOR_ENABLE: 'true'
    EF_OUTPUT_MONITOR_INTERVAL: 15

Before starting these containers, in the .env file, change the values of ELASTIC_PASSWORD and KIBANA_PASSWORD to strong passwords. If necessary also change in the same file the value of MEM_LIMIT (in bytes) to suit your needs (i.e 8589934592). It may also be necessary to increase the value of the kernel parameter vm.max_map_count to at least 262144 (https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_set_vm_max_map_count_to_at_least_262144).

To start these containers, install the latest versions of docker and docker compose, then change into the directory of this project and run:

    docker compose up

After the containers are up and running, you can access the Kibana dashboard here:

    http://<IP of host where containers are running>:5601

From the Kibana dashboard, you can login with the credentials:

    username: elastic
    password: <the value you set for the ELASTIC_PASSWORD variable in the .env file>

The elastiflow ndjson can be downloaded from here https://docs.elastiflow.com/docs/data_platforms/elastic/kibana/. Instructions to import the ndjson from kibana are available in this video (timestamp 6:17): https://youtu.be/OB7tWPthBI0?t=377

The same ndjson kibana-8.2.x-flow-codex.ndjson that can be downloaded from elastiflow's website linked above is provided in this repo just for convenience.

