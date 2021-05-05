FROM amazonlinux:2
MAINTAINER Ken DeLong "kenwdelong@gmail.com"

ENV WORK="/work" \
    ANSIBLE_VERSION=3.3.0 \
    LANG=en_US.utf8 \
    LC_ALL=en_US.utf8

RUN yum -y update &&\ 
    yum clean all && \
    rm -rf /var/cache/yum

RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py && python get-pip.py  &&\
    pip install ansible==$ANSIBLE_VERSION &&\
    ansible-galaxy collection install amazon.aws  &&\
    ansible-galaxy collection install community.aws  &&\
    pip install awscli &&\
    pip install boto boto3 botocore
RUN mkdir $WORK && \
    chmod 0777 $WORK
WORKDIR $WORK
ENTRYPOINT ["ansible-playbook"]