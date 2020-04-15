# Metadata Services Deployment

***Note: This work has been incorporated into, and superseded by, the [Open Data Platform](https://github.com/SAEONData/Open-Data-Platform) project.***

Docker-based deployment of metadata services, including:

- CKAN metadata management server
- PyCSW metadata harvest endpoint
- Elasticsearch metadata discovery catalogue
- and related dependencies

## System configuration
The following command needs to be run on the host in order for the elasticsearch container to work:

    sudo sysctl -w vm.max_map_count=262144

To make the change permanent, edit the file `/etc/sysctl.conf` and add the following line:

    vm.max_map_count=262144

## Configuration
Create a `.env` file in the install directory and set the following environment variables,
which are injected into the CKAN configuration:

- **`SERVER_ENV`**: deployment environment: `development`|`testing`|`staging`|`production`
- **`CKAN_URL`**: public URL of the CKAN server
- **`CKAN_DB_URL`**: connection string for the CKAN database
- **`DOI_PREFIX`**: SAEON DOI prefix
- **`HYDRA_PUBLIC_URL`**: URL of the Hydra public API
- **`HYDRA_ADMIN_URL`**: URL of the Hydra admin API
- **`OAUTH2_CLIENT_SECRET`**: client secret for the CKAN UI, as registered in Hydra
- **`IDENTITY_SERVICE_URL`**: URL of the [ODP Identity](https://github.com/SAEONData/ODP-Identity) service

## Installation / upgrade
Run the following in the install directory:
    
    docker-compose down
    docker-compose build --no-cache
    docker-compose up -d
