FROM amazonlinux:2023.5.20240624.0   
# Using the above image, which does not match all.yml, because that's the closest tag available
# Tags are here: https://hub.docker.com/_/amazonlinux/tags
MAINTAINER kenwdelong
# Based on cooniur/java

ENV JAVA_VERSION=21.0.4 \
    ZULU_VERSION=21.36.17-ca \
    JAVA_HOME=/usr/local/java \
    TMP_DIR=/tmp/java \
    TMP_FILE=$TMP_DIR/java.tar.gz

RUN dnf -y update &&\ 
    dnf -y install wget tar sudo bash-completion less openssh openssh-clients openssl openssl-pkcs11 sudo wget zip unzip vi vim  && \
    dnf clean all && \
    rm -rf /var/cache/yum &&\
    mkdir -p $JAVA_HOME && \
	  mkdir -p $TMP_DIR && \
    wget --quiet --output-document="$TMP_FILE" \
        --no-cookies --no-check-certificate \
        "https://cdn.azul.com/zulu/bin/zulu${ZULU_VERSION}-jdk${JAVA_VERSION}-linux_x64.tar.gz" && \
    tar -xf "$TMP_FILE" --directory="$JAVA_HOME" --strip-components 1 && \
    rm "$TMP_FILE"

# If I set the path up above with the other ENV vars, it doesn't work.
ENV PATH $JAVA_HOME/bin:$PATH
