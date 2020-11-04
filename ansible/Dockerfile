FROM amazonlinux:2
MAINTAINER Ken DeLong "kenwdelong@gmail.com"

ENV WORK="/work" \
    LANG=en_US.utf8 \
    LC_ALL=en_US.utf8

RUN yum -y update &&\ 
    yum clean all && \
    rm -rf /var/cache/yum

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python get-pip.py
RUN pip install ansible
RUN ansible-galaxy collection install community.aws
RUN mkdir $WORK && \
    chmod 0777 $WORK
WORKDIR $WORK
ENTRYPOINT ["ansible-playbook"]