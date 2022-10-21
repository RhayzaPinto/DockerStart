FROM redhat/ubi8:8.5

LABEL maintainer="Rhayza rhayzapinto@gmail.com"

EXPOSE 8080

RUN yum install -y httpd

COPY src /var/www/html/index.html

CMD ["httpd", "-D", "FOREGROUND"]