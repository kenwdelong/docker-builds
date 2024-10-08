FROM amazonlinux:2023.5.20240624.0 
MAINTAINER Ken DeLong "kenwdelong@gmail.com"

#RUN dnf -y install glibc-locale-source glibc-langpack-en  &&\
#    localedef -v -c -i en_US -f UTF-8 en_US.UTF-8
# We used to have the locale as en_US.UTF-8, but that is not working.  The localedef call above works on an EC2 instance with Amazon Linux 2023, but not in the docker image.

ENV WORK="/work" \
    ANSIBLE_VERSION=10.2.0 \
    PYTHON_VERSION=3.11 \
    PYTHON_SYSTEM_VERSION=3.9 \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8

RUN dnf -y install bash-completion less openssh openssh-clients openssl openssl-pkcs11 sudo wget zip unzip python${PYTHON_VERSION} 

# system version
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python${PYTHON_SYSTEM_VERSION} get-pip.py

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python${PYTHON_VERSION} get-pip.py  &&\
    pip${PYTHON_VERSION} install ansible==$ANSIBLE_VERSION &&\
    pip${PYTHON_VERSION} install awscli packaging &&\                  # I think adding "packaging" here will stop the error on the route53 module
    pip${PYTHON_SYSTEM_VERSION} install boto boto3 botocore   &&\      # want it for both "system python" (3.9) and 3.11
    pip${PYTHON_VERSION} install boto boto3 botocore

RUN mv /etc/localtime /etc/localtime.bak  &&\
    ln -s /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
    
RUN mkdir $WORK && \
    chmod 0777 $WORK
WORKDIR $WORK

ENTRYPOINT ["ansible-playbook"]