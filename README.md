# Metadata Services Deployment

Docker-based deployment of front- and back-end metadata services. This project provides
separate docker-compose files for front- and back-end servers.

_N.B. Back-end containers should not be started on front-end servers and vice versa._

## Back-End

This sets up the CKAN metadata management server, Elasticsearch instance and Elastic search agent on a back-end server.

### System configuration
The following command needs to be run on the host in order for the elasticsearch container to work:

    sudo sysctl -w vm.max_map_count=262144

To make the change permanent, edit the file `/etc/sysctl.conf` and add the following line:

    vm.max_map_count=262144

### Configuration
Create a `.env` file in the install directory and set the following environment variables,
which are injected into the CKAN configuration:

- **`CKAN_URL`**: URL of the CKAN server
- **`CKAN_DB_URL`**: URL of the CKAN database
- **`DOI_PREFIX`**: SAEON DOI prefix
- **`HYDRA_PUBLIC_URL`**: URL of the Hydra public API
- **`HYDRA_ADMIN_URL`**: URL of the Hydra admin API
- **`OAUTH2_CLIENT_SECRET`**: client secret for the CKAN UI, as registered in Hydra
- **`IDENTITY_SERVICE_URL`**: URL of the [ODP Identity](https://github.com/SAEONData/ODP-Identity) service

### Installation / upgrade
Run the following in the install directory:
    
    docker-compose -f back-end.yml down
    docker-compose -f back-end.yml build --no-cache
    docker-compose -f back-end.yml up -d

## Front-End

This sets up PyCSW on a front-end server.

Note: In due course we will add docker config for deploying the CKAN metadata discovery instance.

### Configuration
Create a `.env` file in the install directory and set the following environment variables,
which are injected into the PyCSW configuration:

- **`ELASTIC_AGENT_SEARCH_URL`**: URL of the [Elastic Search Agent](https://github.com/SAEONData/elastic-search-agent)
search API, e.g. `http://es-agent.saeon.dvn/search`

### Installation / upgrade
Run the following in the install directory:
    
    docker-compose -f front-end.yml down
    docker-compose -f front-end.yml build --no-cache
    docker-compose -f front-end.yml up -d
