FROM jasonrivers/nagios:4.5.2  
#       4.4.14 is from ubunutu:22.04
#FROM jasonrivers/nagios:4.4.6   # branch is missing from https://github.com/JasonRivers/Docker-Nagios/tree/master, 4.4.4 was 16.04, 4.4.7 was 20.04
LABEL maintainer="kenwdelong@yahoo.com"

RUN apt update
RUN apt-get --yes install vim &&\
    apt-get clean all

RUN echo 'SetEnv TZ "America/Los_Angeles"' >> /etc/apache2/conf-enabled/nagios.conf
RUN pip install boto tornado

# user id is from all.yml. Nagios was 999
# from https://www.cyberciti.biz/faq/linux-change-user-group-uid-gid-for-all-owned-files/
RUN usermod -u 3002 nagios       &&\
    find / -user 999 ! -path "/proc/*" -exec chown -h nagios {} \;
    #chown -R nagios /opt/nagios  &&\
    #chown -R nagios /orig
    