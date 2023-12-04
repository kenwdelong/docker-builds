FROM jasonrivers/nagios:4.4.14   
#       4.4.14 is from ubunutu:22.04
#FROM jasonrivers/nagios:4.4.6   # branch is missing from https://github.com/JasonRivers/Docker-Nagios/tree/master, 4.4.4 was 16.04, 4.4.7 was 20.04
MAINTAINER kenwdelong@yahoo.com

RUN apt update
RUN apt-get --yes install python2 vim &&\
    apt-get clean all
RUN ln -s /usr/bin/python2 /usr/bin/python

RUN echo 'SetEnv TZ "America/Los_Angeles"' >> /etc/apache2/conf-enabled/nagios.conf
RUN wget https://bootstrap.pypa.io/pip/2.7/get-pip.py    &&\
    python get-pip.py                            &&\
    rm get-pip.py                                &&\
    pip install boto tornado

# user id is from all.yml. Nagios was 999
# from https://www.cyberciti.biz/faq/linux-change-user-group-uid-gid-for-all-owned-files/
RUN usermod -u 3002 nagios       &&\
    find / -user 999 ! -path "/proc/*" -exec chown -h nagios {} \;
    #chown -R nagios /opt/nagios  &&\
    #chown -R nagios /orig
    