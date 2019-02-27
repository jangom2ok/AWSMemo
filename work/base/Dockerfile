FROM centos:6

RUN yum -y update; yum clean all; \
    groupadd -g 501 webuser; \
    useradd -m -g 501 -u 501 -s /bin/bash webuser; \
    yum -y install httpd; \
    yum -y install wget; \
    wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm; \
    rpm -ivh epel-release-6-8.noarch.rpm; \
    rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm; \
    yum -y install --enablerepo=remi,remi-php56 php php-devel php-mbstring php-pdo php-gd php-xml php-mcrypt libjpeg-devel libpng-devel libXpm-devel freetype-devel

EXPOSE 80

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
