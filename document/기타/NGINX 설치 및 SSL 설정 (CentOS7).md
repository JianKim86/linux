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

ngork

로컬서버를 공개 인터넷에 노출 시키는 도구, 로컬에 실행중인 서버를 안전하게 외부에서 접근가능하도록 해줌

```
# yum install snapd
# systemctl enable --now snapd.socket
# ln -s /var/lib/snapd/snap /snap
# exec bash
# snap install ngrok
# ngrok http test-001.com:80 //ngrok 켜기
```

NGINX 설정 파일 수정

인증서를 발급 받기 위해서는 도메인이 필요

Nginx 기본 설정 파일인 **default.conf** 파일을 열어서 도메인을 추가

```
# vi /etc/nginx/conf.d/default.conf
server {
	listen 80;
	server_name test-001.com;
	
	localtion ~ /\.well-known/acme-challenge/ {
		allow all;
		root /data/front/letsencrypt;
	}
}
```

hosts 파일 수정

서버에서 test-001.com url을 알 수있도록 hosts 파일 수정

```
# vi /etc/hosts
127.0.0.1 test-001.com
```

NGINX 재시작

인증서 발급받기

```
# certbot --webroot -d 4ca87f8a31fe.ngrok.io certonly
```

