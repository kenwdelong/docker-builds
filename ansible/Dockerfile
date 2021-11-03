FROM amazonlinux:2
MAINTAINER Ken DeLong "kenwdelong@gmail.com"

ENV WORK="/work" \
    ANSIBLE_VERSION=4.8.0 \
    LANG=en_US.utf8 \
    LC_ALL=en_US.utf8

RUN yum -y update && \
    yum clean all && \
    rm -rf /var/cache/yum

RUN amazon-linux-extras enable python3.8

RUN amazon-linux-extras enable python3.8  && \
    yum clean metadata && \
    yum -y install python38
    
RUN ln -s /usr/bin/python3.8  /usr/bin/python3
    

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python3 get-pip.py  &&\
    pip install ansible==$ANSIBLE_VERSION &&\
    pip install awscli &&\
    pip install boto boto3 botocore
RUN mkdir $WORK && \
    chmod 0777 $WORK
WORKDIR $WORK
ENTRYPOINT ["ansible-playbook"]