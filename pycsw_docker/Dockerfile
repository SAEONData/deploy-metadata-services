FROM ubuntu:18.04
#RUN add-apt-repository main \
#    add-apt-repository universe \
#    add-apt-repository restricted \
#    add-apt-repository multiverse
RUN apt-get update
RUN apt-get install -y python-pip git libgeos-dev libxml2-dev libxslt1-dev
RUN mkdir /var/www/ && cd /var/www/ && git clone -b elastic https://github.com/SAEONData/pycsw.git


RUN cd /var/www/pycsw/ && pip install -e . && pip install -r requirements-standalone.txt
RUN cd /var/www/pycsw/ && pip install -r requirements-dev.txt
COPY default.cfg /var/www/pycsw/

CMD sleep 40 && python /var/www/pycsw/pycsw/wsgi.py
