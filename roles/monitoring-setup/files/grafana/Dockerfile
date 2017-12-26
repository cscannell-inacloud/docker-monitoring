FROM centos:centos7

LABEL creator="odiadom - Óscar Díaz Domínguez"
LABEL maintainer="DevOpsTF - DevOps Tenerife"

ARG GRAFANA_VERSION=4.6.3
ARG GRAFANA_DOWNLOAD_URL=https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-${GRAFANA_VERSION}-1.x86_64.rpm

RUN yum update -y && \
    yum install -y wget

RUN wget ${GRAFANA_DOWNLOAD_URL} && \
    yum localinstall -y grafana-${GRAFANA_VERSION}-1.x86_64.rpm 

WORKDIR /etc/grafana

ENTRYPOINT [ "/usr/sbin/grafana-server", "--homepath=/usr/share/grafana" ]
