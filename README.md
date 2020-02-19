# Metadata Services Deployment

Docker-based deployment of front- and back-end metadata services. This project provides
separate docker-compose files for front- and back-end servers. Back-end containers should
not be started on front-end servers and vice versa.

## Back-End

This sets up the Elasticsearch instance and Elastic search agent on a back-end server.

Note: In due course we will add docker config for deploying the CKAN metadata management instance.

### Configuration
You may need to run this on the host for the elasticsearch container to start:

    sudo sysctl -w vm.max_map_count=262144

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
