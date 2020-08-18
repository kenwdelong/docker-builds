FROM amazonlinux:2
MAINTAINER Ken DeLong "kenwdelong@gmail.com"

ENV WORK="/work"

RUN yum -y update &&\ 
    yum clean all && \
    rm -rf /var/cache/yum

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python get-pip.py
RUN pip install ansible==2.9.12
RUN mkdir $WORK && \
    chmod 0777 $WORK
WORKDIR $WORK
ENTRYPOINT ["ansible-playbook"]