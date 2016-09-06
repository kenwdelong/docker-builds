FROM cpuguy83/nagios
MAINTAINER kenwdelong@yahoo.com
RUN sed -i 's,UTC,America/Los_Angeles,' /etc/apache2/conf.d/nagios.conf
RUN wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py    &&\
    python get-pip.py                                                 &&\
    rm get-pip.py                                                     &&\
    pip install boto tornado pyopenssl ndg-httpsclient pyasn1 urllib3
