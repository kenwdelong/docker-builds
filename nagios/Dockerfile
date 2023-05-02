FROM jasonrivers/nagios:4.4.6
MAINTAINER kenwdelong@yahoo.com
RUN apt-get --yes install python vi vim &&\
    apt-get clean all
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
    