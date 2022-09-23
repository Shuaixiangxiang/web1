FROM ubuntu:14.04

MAINTAINER 1ZAYAK1

ENV REFRESHED_AT 2022/9/23

ENV LANG C.UTF-8
#更换源
RUN sed -i 's/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirrors.163.com\/ubuntu\//g' /etc/apt/sources.list
#更新
RUN apt-get update -y
#防止Apache安装过程中地区的设置出错
ENV DEBIAN_FRONTEND noninteractive

# 如 安装mysql
RUN apt-get -y install mysql-server
# 安装apache2
RUN apt-get -yqq install apache2
# 安装php7.2.5
RUN apt-get -yqq install php7.2.5 libapache2-mod-php7.2.5
# 安装php扩展
RUN apt-get install -yqq php7-mysql php7-curl php7-gd php7-intl php-pear php7-imagick php7-imap php7-mcrypt php7-memcache php7-ming php7-ps php7-pspell php7-recode php7-snmp php7-sqlite php7-tidy php7-xmlrpc php7-xsl
#配置Apache信息
RUN echo "ServerName localhost:80" >> /etc/apache2/apache2.conf
#移除Apache初始界面
RUN rm -rf /var/www/html/index.html

RUN sed -i 's/Options Indexes FollowSymLinks/Options None/' /etc/apache2/apache2.conf
#复制本地www文件夹下的文件到apache的网站目录
ADD ./tp6 /var/www/html

COPY start.sh /root/start.sh

RUN chmod +x /root/start.sh

ENTRYPOINT cd /root; ./start.sh

EXPOSE 80
