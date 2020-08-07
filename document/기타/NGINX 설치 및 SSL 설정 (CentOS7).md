### NGINX 설치 및 SSL 설정 (CentOS7)

#### 1. NGINX 설치 및 시작

CentOS7 환경에서 NGINX를 설치 하기 위해서는 'epel-release' 라는 rpm을 설치해주어야한다.

epel-release rpm 설치

```
# yum -y install epel-release
```

NGINX repo 등록

```
# vi /etc/yum.repos.d/nginx.repo
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gqgcheck=0
enabled=1
```

NGINX 설치 및 서비스 등록

```
# yum -y install nginx
// NGINX를 부팅 시 실행시키는 심볼릭 링크를 생성하고, NGINX를 시작한다.
# systemctl enable nginx
# systemctl start nginx
//확인: ifconfig 로 ip 확인후 브라우저 접속
# ifconfig
//크롬 브라우저 열기
# /usr/bin/google-chrome --no-sandbox
```

certbot 설치

```
# yum install certbot
# yum install python2-certbot-nginx
```

NGINX 설정 파일 수정

인증서를 발급 받기 위해서는 도메인이 필요

Nginx 기본 설정 파일인 **default.conf** 파일을 열어서 도메인을 추가

```
# vi /etc/nginx/conf.d/default.conf
server {
	listen 80;
	server_name test-001.com;
	location / {
		root /data/front/letsencrypy;
		index index.html index.htm;
	}
	location ~ /\.well-known/acme-challenge/ {
		allow all;
		root /data/front/letsencrypt;
	}
}
# mkdir -p /data/front/letsencrypt
# /data/front/letsencrypt에 index.html 생성
# mkdir -p /usr/share/html/well-known/acme-challenge
```

방화벽  포트추가와 접근권한 추가

```
# chcon -R -t httpd_sys_rw_content_t [index file이 위치한 폴더]
# firewall-cmd --permanent --zone=public --add-port=8080/tcp //추가
# firewall-cmd --reload //리로드
# firewall-cmd --list-ports //확인
```

hosts 파일 수정

서버에서 test-001.com url을 알 수있도록 hosts 파일 수정

```
# vi /etc/host
127.0.0.1 test-001.com
```

NGINX 재시작

ngork

로컬서버를 공개 인터넷에 노출 시키는 도구, 로컬에 실행중인 서버를 안전하게 외부에서 접근가능하도록 해줌

```
# yum install snapd
# systemctl enable --now snapd.socket
# ln -s /var/lib/snapd/snap /snap
# exec bash
# snap install ngrok
## ngrok http test-001.com:80 //ngrok 켜기, default server로 가상도메인이생성됨
# ngrok http -host-header=test-001.com 80 // 원하는 server로 도메인 생성
```

인증서 발급받기

```
# certbot --webroot -d [ngrok 임시 도메인] certonly
```

`--webroot` 옵션을 사용할 경우 플러그인을 찾지못해 경로를 물어본다. 이때 `location ~ /\.well-known/acme-challenge/` 에 설정한 root 경로를 입력하면 된다.

Nginx에 SSL설정

```
#필수사항
server{ 
listen 443 ssl;
ssl_certificate /etc/letsencrypt/live/[ngrok 임시도메인]/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/[ngrok 임시도메인]/privkey.pem;
}
```

https://test-001.com 으로 접속시 에러가 발생한 경우

let's encrypt로부터 인증 받은 도메인과 test-001.com 도메인과 다르기 때문에 발생한 오류이다. 실제 도메인으로 하면  문제가 되지않는다고한다.

인증서 발급 대상과 발급자 확인

