FROM kenwdelong/java:java-8u92
MAINTAINER kenwdelong
# Inspired by cooniur

# Version
ENV MAVEN_VERSION=3.3.9 \
    MAVEN_HOME=/usr/local/maven \
    JENKINS_INSTALL=/usr/local/jenkins/bin \
    JENKINS_HOME=/jenkins \
    JENKINS_TIMEZONE=America/Los_Angeles \
    MAVEN_TMP_FILE=/tmp/maven.tar.gz \
    GET_PIP_FILE=/tmp/get-pip.py

# Timezone
RUN  mv /etc/localtime /etc/localtime.bak && ln -s /usr/share/zoneinfo/${JENKINS_TIMEZONE} /etc/localtime
    
# Install Maven
RUN mkdir -p $MAVEN_HOME &&\
    wget --quiet --output-document=$MAVEN_TMP_FILE \
        "http://www.us.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz" &&\
    tar -xf "$MAVEN_TMP_FILE" --directory="$MAVEN_HOME" --strip-components 1 &&\
    rm $MAVEN_TMP_FILE

# Install EPEL-RELEASE, GIT
RUN yum -y install git epel-release gcc python-devel libffi-devel openssl-devel && yum clean all

# Install Ansible, AWS-CLI, Boto (AWS lib in Python)
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "$GET_PIP_FILE" &&\
    python $GET_PIP_FILE &&\
    pip install --upgrade ansible &&\
    pip install awscli &&\
    pip install boto &&\
    rm -f $GET_PIP_FILE &&\
    rm -rf /tmp/pip_build_root


ENV JENKINS_VERSION=2.7.1

# Install Jenkins
RUN mkdir -p $JENKINS_HOME &&\
    mkdir -p $JENKINS_INSTALL &&\
    wget --quiet --output-document=$JENKINS_INSTALL/jenkins.war "http://mirrors.jenkins-ci.org/war-stable/$JENKINS_VERSION/jenkins.war" &&\
    chmod 0644 $JENKINS_INSTALL/jenkins.war

# Jenkins' home is in /jenkins

ENV PATH $MAVEN_HOME/bin:$PATH

EXPOSE 8080

RUN useradd -r -u 201 -m -c "jenkins role account" -d /home/jenkins -s /bin/false jenkins
RUN chown jenkins $JENKINS_HOME
USER jenkins

CMD java -jar -Dorg.apache.commons.jelly.tags.fmt.timeZone=$JENKINS_TIMEZONE $JENKINS_INSTALL/jenkins.war

