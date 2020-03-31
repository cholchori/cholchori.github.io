---
title: 우분투 서버 라즈베리 파이 설정
layout: post
date: 2020-03-31
categories: ["IT"]
---
# 재부팅시 fsck
* root 로 로그인
<pre>touch /forcefsck</pre>
* reboot

# WiFi 설정
* SSID 접속
<pre>nmcli d 
nmcli r wifi on 
nmcli d wifi list 
nmcli d wifi connect my_wifi password <password></pre>
* Hidden SSID 접속
<pre>nmcli c add type wifi con-name <name> ifname wlan0 ssid <ssid> 
nmcli c modify <name> wifi-sec.key-mgmt wpa-psk wifi-sec.psk <password> nmcli c up <name></pre>


# locale 바꾸기 
<pre>sudo dpkg-reconfigure locales
sudo update-locale LANG=ko_KR.UTF-8 LC_MESSAGES=POSIX
</pre>

# timezone 변경
<pre>sudo tzselect</pre>

# 5G WiFi 접속 
* 라즈베리파이 기본 설정에서 5G 무선 와이파이 SSID 검색 불가
* 해결책 무선 국가코드를 미국(US)로 설정
* /etc/default/crda 을 편집
:- REGDOMAIN=US 로 설정
* sudo service network-manager restart

# vi color 변경
* vi 컬러때문에 글읽기가 곤란할때
* /usr/share/vim/vim81/colors 에 파일을 보면 적용가능한 color 파일들이(.vim) 있음
* /etc/vim/vimrc 파일에 :colorscheme ron 형태로 원하는 color 이름을 적용

# Nginx php mariaDB 설치 
* 설치
<pre>sudo apt install nginx
sudo systemctl status nginx
sudo systemctl start nginx
sudo ufw app list
sudo ufw app info "Nginx Full"
sudo ufw allow in "Nginx Full"
sudo apt install mariadb-server mariadb-client
sudo systemctl status mysql
mysql_secure_installation
sudo mysql -u root
use mysql;
update user set plugin='' where User='root';
mysql_secure_installation
sudo apt-get install php-fpm php-mysql
sudo vi /etc/php/7.2/fpm/php.ini
;cgi.fix_pathinfo=1 => cgi.fix_pathinfo=0
sudo systemctl status php7.2-fpm
sudo vi /etc/nginx/sites-available/default

add index.php

location ~ \.php$ {
include snippets/fastcgi-php.conf;
#
# # With php-fpm (or other unix sockets):
fastcgi_pass unix:/run/php/php7.2-fpm.sock;
# # With php-cgi (or other tcp sockets):
# fastcgi_pass 127.0.0.1:9000;
}
# deny access to .htaccess files, if Apache's document root
 # concurs with nginx's one
 #
 location ~ /\.ht {
 deny all;
 }
}

sudo nginx -t
sudo systemctl restart nginx
sudo apt-cache search php- | less
sudo apt-cache show php-gd
sudo apt-get install php-gd

sudo apt-get install php*</pre>

* SSL 설정
<pre>server {
  listen 80;
  server_name domain.com;
  rewrite ^ https://$server_name$request_uri? permanent;
}

server {
        # listen 80 default_server;
        # listen [::]:80 default_server;

        listen 443 ssl default_server;
        listen [::]:443 ssl default_server;

        ssl_certificate /etc/nginx/ssl/****-chain.pem;
        ssl_certificate_key /etc/nginx/ssl/****-key.pem;
        ssl_prefer_server_ciphers on;

        server_name domain.com;</pre>

# 서비스 등록 
* /etc/systemd/system/myservice.service 작성
<pre>[Unit] Description=serviceName 

[Service] ExecStart=/path/path/servce.sh 

[Install] WantedBy=multi-user.target</pre>

* 실행
<pre>systemctl enable serviceName 
service serviceName start</pre>
