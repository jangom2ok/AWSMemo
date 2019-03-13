FROM centos:6

RUN yum -y update; yum clean all; \
    yum remove httpd; \
    yum install -y initscripts; \
    groupadd -g 501 webuser; \
    useradd -m -g 501 -u 501 -s /bin/bash webuser; \
    yum -y install wget; \
    cd /etc/yum.repos.d/; \
    wget https://repos.fedorapeople.org/repos/jkaluza/httpd24/epel-httpd24.repo; \
    yum install httpd24; \
    chkconfig httpd24-httpd on; \
    wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm; \
    rpm -ivh epel-release-6-8.noarch.rpm; \
    rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm; \
    yum -y install --enablerepo=remi,remi-php56 php php-devel php-mbstring php-pdo php-gd php-xml php-mcrypt libjpeg-devel libpng-devel libXpm-devel freetype-devel


COPY functions /etc/rc.d/init.d/

COPY httpd.conf
COPY php.ini


EXPOSE 80

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
