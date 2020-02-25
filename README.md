# Metadata Services Deployment

Docker-based deployment of front- and back-end metadata services. This project provides
separate docker-compose files for front- and back-end servers.

_N.B. Back-end containers should not be started on front-end servers and vice versa._

## Back-End

This sets up the CKAN metadata management server, Elasticsearch instance and Elastic search agent on a back-end server.

### System configuration
The following command needs to be run on the host in order for the elasticsearch container to work:

    sudo sysctl -w vm.max_map_count=262144

### Configuration

Create a `.env` file in the install directory and set the following environment variables:

#### CKAN
- **`CKAN_URL`**: URL of the CKAN server
- **`CKAN_DB_URL`**: URL of the CKAN database
- **`DOI_PREFIX`**: SAEON DOI prefix
- **`ELASTIC_AGENT_URL`**: URL of the [Elastic Search Agent](https://github.com/SAEONData/elastic-search-agent)
- **`HYDRA_PUBLIC_URL`**: URL of the Hydra public API
- **`HYDRA_ADMIN_URL`**: URL of the Hydra admin API
- **`OAUTH2_CLIENT_SECRET`**: client secret for the CKAN UI, as registered in Hydra
- **`IDENTITY_SERVICE_URL`**: URL of the [ODP Identity](https://github.com/SAEONData/ODP-Identity) service

#### Elastic Search Agent
- **`ELASTIC_AGENT_HOST`**: hostname / IP address of the agent
- **`ELASTIC_AGENT_PORT`**: port number of the agent
- **`ELASTIC_SEARCH_HOST`**: hostname / IP address of the Elasticsearch instance
- **`ELASTIC_SEARCH_PORT`**: port number of the Elasticsearch instance (usually `9200`)

### Installation / upgrade
Run the following in the install directory:
    
    sudo docker-compose -f back-end.yml down
    sudo docker-compose -f back-end.yml build --no-cache
    sudo docker-compose -f back-end.yml up -d

## Front-End

This sets up PyCSW on a front-end server.

Note: In due course we will add docker config for deploying the CKAN metadata discovery instance.

### Configuration
Set the `repository.filter` option in pycsw_docker/default.cfg to point to
the Elastic search agent search API, e.g.
    
    [repository]
    filter=http://es.saeon.dvn/search

### Installation / upgrade
Run the following in the install directory:
    
    sudo docker-compose -f front-end.yml down
    sudo docker-compose -f front-end.yml build --no-cache
    sudo docker-compose -f front-end.yml up -d
