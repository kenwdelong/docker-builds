FROM kenwdelong/java:java-21.0.4
MAINTAINER kenwdelong
# Inspired by cooniur

# Version
# Look here for jenkins http://mirrors.jenkins.io/war-stable/
# Python https://docs.aws.amazon.com/linux/al2023/ug/python.html
# Ansible 10.2.0 requires Python 3.10 or greater
ENV MAVEN_VERSION=3.9.8 \
    MAVEN_HOME=/usr/local/maven \
    MAVEN_TMP_FILE=/tmp/maven.tar.gz \
    ANSIBLE_VERSION=10.2.0 \
    JENKINS_VERSION=2.452.3 \
    PYTHON_VERSION=3.11 \
    JENKINS_INSTALL=/usr/local/jenkins/bin \
    JENKINS_HOME=/jenkins \
    JENKINS_TIMEZONE=America/Los_Angeles \
    GET_PIP_FILE=/tmp/get-pip.py \
    J2OBJC_VERSION=1.3.1 \
    J2OBJC_INSTALL_DIR=/opt \
    J2OBJC_TMP_FILE=/tmp/j2objc.zip \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8
    

# Timezone
RUN  mv /etc/localtime /etc/localtime.bak && ln -s /usr/share/zoneinfo/${JENKINS_TIMEZONE} /etc/localtime
    
# Install extra packages
RUN dnf -y install dejavu-sans-fonts fontconfig git wget gcc python${PYTHON_VERSION}-devel libffi-devel openssl-devel unzip net-tools procps-ng python${PYTHON_VERSION} &&\
    dnf clean all &&\
    rm -rf /var/cache/yum

# Install Maven  
RUN mkdir -p $MAVEN_HOME  && \
    wget --quiet --output-document=$MAVEN_TMP_FILE \
        "https://dlcdn.apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz"  && \ 
    tar -xf "$MAVEN_TMP_FILE" --directory="$MAVEN_HOME" --strip-components 1  && \
    rm $MAVEN_TMP_FILE

# Install Ansible, AWS-CLI, Boto (AWS lib in Python)
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "$GET_PIP_FILE" &&\
    python${PYTHON_VERSION} $GET_PIP_FILE &&\
    pip${PYTHON_VERSION} install ansible==$ANSIBLE_VERSION &&\
    pip${PYTHON_VERSION} install awscli &&\
    pip${PYTHON_VERSION} install boto boto3 botocore &&\
    rm -f $GET_PIP_FILE &&\
    rm -rf /tmp/pip_build_root

# Install Jenkins
RUN mkdir -p $JENKINS_HOME &&\
    mkdir -p $JENKINS_INSTALL &&\
    wget --quiet --output-document=$JENKINS_INSTALL/jenkins.war "https://mirrors.jenkins.io/war-stable/$JENKINS_VERSION/jenkins.war" &&\
    chmod 0644 $JENKINS_INSTALL/jenkins.war

# Jenkins' home is in /jenkins

ENV PATH $MAVEN_HOME/bin:$PATH

EXPOSE 8080

RUN useradd -r -u 201 -m -c "jenkins role account" -d /home/jenkins -s /bin/false jenkins
RUN chown jenkins $JENKINS_HOME
USER jenkins

CMD java -Xmx2048m -Dorg.apache.commons.jelly.tags.fmt.timeZone=$JENKINS_TIMEZONE -jar $JENKINS_INSTALL/jenkins.war
