## PRE-INSTALLATION CONFIGURATION: ##
- Set ELASTIC_SEARCH_HOST in agent_docker/env_vars.sh
- Set the following in pycsw_docker/default.cfg:
    repository.filter = <ELASTIC_AGENT_HOST:AGENT_PORT>
    E.g repository.filter=http://10.0.2.15:9210:9210/search

## INSTALLATION: ##
Run the following in the install directory
- $<INSTALL_DIR> docker-compose build
- $<INSTALL_DIR> mkdir elastic-data
- $<INSTALL_DIR> chmod 777 elastic-data

## PRE-RUN CONFIGURATION: ##
You may need to run this on the host for the elastic search docker to start:
- sudo sysctl -w vm.max_map_count=262144

## RUNNING THE SERVICES: ##
Run the following in the install directory
- $<INSTALL_DIR> docker-compose up -d

## INITIALISING THE SEARCH INDEX ##
Once the services are up and running, run the following on the hostL
- docker exec -it search_agent python /tmp/elastic-search-agent/agent/tests/test_create_index.py
- docker exec -it search_agent python /tmp/elastic-search-agent/agent/tests/test_add.py

## TESTING: ##
Open a web browser and enter the following urls:
### 1) http://<ELASTIC_SEARCH_HOST>:9200/ ###
- You should see something like this:
name	"LHFiJcO"
cluster_name	"docker-cluster"
cluster_uuid	"HbYOC9NSQUadMQrJG8_KhQ"
version	{…}
tagline	"You Know, for Search"

### 2) http://<ELASTIC_AGENT_HOST:9210> ###
- You should see something like this:
Welcome to the SAEON Metadata Search Agent
JSON API
Create Index
Create an index
.. etc

 ### 3) http://127.0.0.1:8000/?service=CSW&version=2.0.2&request=GetRecords&typenames=csw:Record&elementsetname=full&resulttype=results&SortBy=dc:publisher:D ###

- You should see something like this:
<csw:GetRecordsResponse version="2.0.2" xsi:schemaLocation="http://www.opengis.net/cat/csw/2.0.2 http://schemas.opengis.net/csw/2.0.2/CSW-discovery.xsd"><csw:SearchStatus timestamp="2019-03-20T12:02:42Z"/><csw:SearchResults nextRecord="0" numberOfRecordsMatched="2" numberOfRecordsReturned="2" recordSchema="http://www.opengis.net/cat/csw/2.0.2" elementSet="full"><csw:Record><dc:identifier>10.5072.2</dc:identifier><dc:title>Second Full DataCite XML Example</dc:title><dc:type>service</dc:type><dc:subject>101 computer science</dc:subject> ... etc
