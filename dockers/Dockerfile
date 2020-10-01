FROM centos:8

MAINTAINER Python Server

COPY . /app/python
#
RUN yum -y install epel-release
RUN yum -y install httpd
RUN dnf -y install python3-mod_wsgi

#RUN yum -y groupinstall "Development Tools"
RUN dnf -y install python3
RUN yum -y install gcc openssl-devel bzip2-devel libffi-devel
RUN yum -y install python3-pip
RUN yum -y install epel-release iproute at curl crontabs

RUN pip3 install django

# install ssl
RUN dnf -y install mod_ssl
ADD dockers/ssl /etc/httpd/ssl

EXPOSE 80
EXPOSE 443

WORKDIR /app/python

# config port 80
ADD dockers/vhost.conf /etc/httpd/conf.d/welcome.conf

# config port 443
ADD dockers/ssl.conf /etc/httpd/conf.d/ssl.conf

RUN systemctl enable httpd \
 && systemctl enable crond

CMD ["/sbin/init"]