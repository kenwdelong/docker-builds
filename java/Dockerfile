FROM krallin/centos-tini:centos7
MAINTAINER kenwdelong
# Based on cooniur/java

ENV JAVA_VERSION=8u92 \
    JAVA_LONG_VERSION=8u92-b14 \
    JAVA_HOME=/usr/local/java \
    TMP_DIR=/tmp/java \
    TMP_FILE=$TMP_DIR/java.tar.gz

RUN yum -y install wget tar sudo && \
    yum clean all && \
    mkdir -p $JAVA_HOME && \
	mkdir -p $TMP_DIR && \
    wget --quiet --output-document="$TMP_FILE" \
        --no-cookies --no-check-certificate \
        --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
        "http://download.oracle.com/otn-pub/java/jdk/$JAVA_LONG_VERSION/server-jre-$JAVA_VERSION-linux-x64.tar.gz" && \
    tar -xf "$TMP_FILE" --directory="$JAVA_HOME" --strip-components 1 && \
    rm "$TMP_FILE"

# If I set the path up above with the other ENV vars, it doesn't work.
ENV PATH $JAVA_HOME/bin:$PATH
