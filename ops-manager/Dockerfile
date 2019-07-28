FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

ENV OPS_MGR_VERSION=4.0.13.50537.20190703T1029Z-1
RUN echo 'Acquire::http::Proxy "http://172.17.0.1:3128";' | tee /etc/apt/apt.conf.d/01proxy

RUN apt-get update 
RUN apt-get install -y wget nano curl libsasl2-2 ca-certificates libsnmp30 libgssapi-krb5-2 libkrb5-dbg libldap-2.4-2 libpcap0.8 openssl \
#RUN apt-get update && apt-get install -y apt-utils wget nano curl libsasl2-2 libsnmp30 ca-certificates libcurl4 libgssapi-krb5-2 libkrb5-dbg libldap-2.4-2 libpcap0.8 snmp openssl
  && curl -O  https://downloads.mongodb.com/on-prem-mms/deb/mongodb-mms_${OPS_MGR_VERSION}_x86_64.deb \
  && dpkg --install --no-triggers mongodb-mms_${OPS_MGR_VERSION}_x86_64.deb 
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /*.deb

#COPY mongodb-mms_4.0.13.50537.20190703T1029Z-1_x86_64.deb /tmp/
#RUN dpkg --install --no-triggers /tmp/mongodb-mms_4.0.13.50537.20190703T1029Z-1_x86_64.deb

COPY conf-mms.properties /opt/mongodb/mms/conf/conf-mms.properties
COPY docker-entrypoint.sh /entrypoint.sh
VOLUME /etc/mongodb-mms /opt/mongodb/mms/conf /opt/mongodb/mms/logs


ENTRYPOINT ["/entrypoint.sh"]

CMD ["mongodb-mms"]