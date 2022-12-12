FROM kenwdelong/java:java-17.0.5
MAINTAINER kenwdelong
# Inspired by cooniur

# Version
# Look here for jenkins http://mirrors.jenkins.io/war-stable/
ENV MAVEN_VERSION=3.8.6 \
    MAVEN_HOME=/usr/local/maven \
    MAVEN_TMP_FILE=/tmp/maven.tar.gz \
    ANSIBLE_VERSION=6.6.0 \
    JENKINS_VERSION=2.361.1 \
    JENKINS_INSTALL=/usr/local/jenkins/bin \
    JENKINS_HOME=/jenkins \
    JENKINS_TIMEZONE=America/Los_Angeles \
    GET_PIP_FILE=/tmp/get-pip.py \
    J2OBJC_VERSION=1.3.1 \
    J2OBJC_INSTALL_DIR=/opt \
    J2OBJC_TMP_FILE=/tmp/j2objc.zip \
    LANG=en_US.utf8 \
    LC_ALL=en_US.utf8
    
# The above locale variables were inserted Aug 18, 2020 to combat a bug in PIP 20.2 	https://github.com/pypa/pip/issues/8658        

# Timezone
RUN  mv /etc/localtime /etc/localtime.bak && ln -s /usr/share/zoneinfo/${JENKINS_TIMEZONE} /etc/localtime
    
# Install EPEL-RELEASE, GIT
RUN yum -y install dejavu-sans-fonts fontconfig git wget epel-release gcc python-devel libffi-devel openssl-devel unzip &&\
    yum clean all &&\
    rm -rf /var/cache/yum

# Install Maven  
RUN mkdir -p $MAVEN_HOME  && \
    wget --quiet --output-document=$MAVEN_TMP_FILE \
        "https://dlcdn.apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz"  && \ 
    tar -xf "$MAVEN_TMP_FILE" --directory="$MAVEN_HOME" --strip-components 1  && \
    rm $MAVEN_TMP_FILE

#  == Python 3.8 ==
RUN amazon-linux-extras enable python3.8

RUN amazon-linux-extras enable python3.8  && \
    yum clean metadata && \
    yum -y install python38
    
RUN ln -s /usr/bin/python3.8  /usr/bin/python3
    

# Install Ansible, AWS-CLI, Boto (AWS lib in Python)
#RUN curl "https://bootstrap.pypa.io/pip/2.7/get-pip.py" -o "$GET_PIP_FILE" &&\
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "$GET_PIP_FILE" &&\
    python3 $GET_PIP_FILE &&\
    pip install ansible==$ANSIBLE_VERSION &&\
    pip install awscli &&\
    pip install boto boto3 botocore &&\
    rm -f $GET_PIP_FILE &&\
    rm -rf /tmp/pip_build_root

# Install Jenkins
RUN mkdir -p $JENKINS_HOME &&\
    mkdir -p $JENKINS_INSTALL &&\
    wget --quiet --output-document=$JENKINS_INSTALL/jenkins.war "https://mirrors.jenkins.io/war-stable/$JENKINS_VERSION/jenkins.war" &&\
    chmod 0644 $JENKINS_INSTALL/jenkins.war

# Jenkins' home is in /jenkins


# Install j2objc. Since we are only translating, we don't need the mac libs.  Saves 500MB.
#RUN wget --quiet --output-document=$J2OBJC_TMP_FILE "https://github.com/google/j2objc/releases/download/${J2OBJC_VERSION}/j2objc-${J2OBJC_VERSION}.zip" &&\
#    unzip "$J2OBJC_TMP_FILE" -d "$J2OBJC_INSTALL_DIR" &&\ 
#    ln -s "${J2OBJC_INSTALL_DIR}/j2objc-${J2OBJC_VERSION}" "${J2OBJC_INSTALL_DIR}/j2objc" &&\
#    rm -rf ${J2OBJC_INSTALL_DIR}/j2objc/lib/maxosx &&\
#    rm -rf ${J2OBJC_INSTALL_DIR}/j2objc/lib/appletvos &&\
#    rm $J2OBJC_TMP_FILE
# Take this out until we someday need to recompile weightlib. This will make the image way smaller


# Install NodeJS
#RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -  &&\
#    sudo yum -y install nodejs
# We don't need to install node - the Jenkins Node Plugin handles it for us!

ENV PATH $MAVEN_HOME/bin:$PATH

EXPOSE 8080

RUN useradd -r -u 201 -m -c "jenkins role account" -d /home/jenkins -s /bin/false jenkins
RUN chown jenkins $JENKINS_HOME
USER jenkins

CMD java -Xmx2048m -Dorg.apache.commons.jelly.tags.fmt.timeZone=$JENKINS_TIMEZONE -jar $JENKINS_INSTALL/jenkins.war
