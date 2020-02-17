FROM python:3.6

RUN mkdir -p /srv
RUN cd /srv && git clone https://github.com/SAEONData/elastic-search-agent
RUN cd /srv/elastic-search-agent && pip install .

CMD ["python", "/srv/elastic-search-agent/bin/agentapi.py"]
