FROM registry.access.redhat.com/ubi8/ubi:8.0 



MAINTAINER Red Hat Training <training@redhat.com>


ENV DOCROOT=/var/www/html 



RUN   yum install -y --disableplugin=subscription-manager httpd && \ 

      yum clean all --disableplugin=subscription-manager -y && \

      echo "Hello from the httpd-parent container!" > ${DOCROOT}/index.html


ONBUILD COPY src/ ${DOCROOT}/ 


EXPOSE 8080

RUN rm -rf /run/httpd && mkdir /run/httpd && \
    chgrp -R 0 ${DOCROOT}/ && \
    chmod -R g=u ${DOCROOT}/  && \
    chgrp -R 0 /run/httpd/ /etc/httpd/ && \
    chmod -R g=u /run/httpd/ /etc/httpd/

RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf && \
    sed -i "s/#ServerName www.example.com:80/ServerName 0.0.0.0:8080/g"  /etc/httpd/conf/httpd.conf

USER 1001 


CMD /usr/sbin/httpd -DFOREGROUND
