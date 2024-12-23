FROM jasonrivers/nagios:4.5.7
#       4.4.14 is from ubunutu:22.04
#FROM jasonrivers/nagios:4.4.6   # branch is missing from https://github.com/JasonRivers/Docker-Nagios/tree/master, 4.4.4 was 16.04, 4.4.7 was 20.04
LABEL maintainer="kenwdelong@yahoo.com"

RUN apt update
RUN apt-get --yes install vim &&\
    apt-get clean all
    
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python3 get-pip.py  &&\
    pip3 install boto boto3 botocore
    

RUN echo 'SetEnv TZ "America/Los_Angeles"' >> /etc/apache2/conf-enabled/nagios.conf

# user id is from all.yml. Nagios was 999
# from https://www.cyberciti.biz/faq/linux-change-user-group-uid-gid-for-all-owned-files/
RUN usermod -u 3002 nagios       &&\
    find / -user 999 ! -path "/proc/*" -exec chown -h nagios {} \;
    #chown -R nagios /opt/nagios  &&\
    #chown -R nagios /orig
    