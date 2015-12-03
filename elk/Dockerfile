FROM sebp/elk:E1L1K4
MAINTAINER kenwdelong@yahoo.com
ADD 01-lumberjack-input.conf /etc/logstash/conf.d/01-lumberjack-input.conf

RUN curl http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz -o /tmp/GeoListCity.dat.gz &&\
    gunzip -c /tmp/GeoLiteCity.dat.gz > /etc/logstash/GeoLiteCity.dat
