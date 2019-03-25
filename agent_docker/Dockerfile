FROM python:3.4

RUN ls /
#RUN ls
RUN cd /tmp/ && git clone https://github.com/SAEONData/elastic-search-agent
COPY env_vars.sh /tmp/
RUN . /tmp/env_vars.sh && sed -i "s/es_domain = 'localhost'/es_domain = '$ELASTIC_SEARCH_HOST'/g" /tmp/elastic-search-agent/agent/config.py

RUN . /tmp/env_vars.sh && sed -i "s/es_port = 9200/es_port = '$ELASTIC_SEARCH_PORT'/g" /tmp/elastic-search-agent/agent/config.py

#RUN sed -i "s/server_domain = 'localhost'/server_domain = '10.0.2.15'/g" /tmp/elastic-search-agent/agent/config.py

RUN cd /tmp/elastic-search-agent/ && python setup.py install

RUN mkdir /scripts/
#CMD touch /tmp/test.txt && tail -f /tmp/test.txt
CMD sleep 30 && python /tmp/elastic-search-agent/bin/agentapi.py
