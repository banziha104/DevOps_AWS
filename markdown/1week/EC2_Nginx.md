# EC2

### 정의 및 특징

- AWS에서 제공하는 가상 서버
- 다양한 OS 제공(Amazon Linux 연구해보기)
- 원하는 사양을 관리자 직접 선택할 수 있음
- 필요할 때마다 사용 / 중지 가능

### 실습

- AMI 선택

![1](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/1.png)

- 보안 그룹설정

![2](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/2.png)

- 키페어 설정

![3](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/3.png)

- EC2 가동확인

![4](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/4.png)

- EC2 접속

![5](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/5.png)

- sudo su 명령어로 루트권한으로 변경
- nginx 1.12 설치
- nginx 실행

![6](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/6.png)
![7](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/7.png)

- 80번 포트열기

![8](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/6.png)
![9](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/9.png)

- dns 주소로 웹 브라우저에서 접속

![10](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/10.png)

    
### Nginx 설정하기

```bash
find / -name nginx.conf # 위치 찾기
cd /etc/nginx # 해당 폴더로 이동
cp nginx.conf nginx-copy.conf # 잘못 수저을 하면 원래 샅애로 백업을 위해 기존 설정 파일 복사
vi nginx.conf # vi 에디터로 nginx.conf 열고 파일 수정하기
nginx -s reload # nginx 재기동
``` 

- 루트 변경
   
```yaml
server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html/Fastcampus-web-deploy; # Nginx 루트 폴더 변경

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        }
         location ~* / (album|signin){ # 정규 표현식과 같이 (album | signin) 에 매칭되는지 확인 후 Nginx root 디렉토리를 해당 블럭에 적힌 디렉토리로 변경
            root /usr/share/nginx/html/Fastcampus-web-deploy/page;
        }
        
        location /api {
            # 들어온 요청을 다른 웹 서버 or WAS로 전달
            # DB서버와 연결되 있는 WAS의 ip와 포트 번호를 감출 수 있음
            proxy_pass {ec2_private_dns/ip}:8080 # 프록시를 
            
        }
```

- ~ / ~* : 들어오는 URL을 정규표현식으로 처리를 위해 사용하는 옵션
    - ~ : 대소문자 구분하여 적용
    - ~* : 대소문자 구분 없이 적용
    
### Nginx 기타 설정

- worker_process auto(or number) : 몇 개의 thread를 사용할지, auto인 경우 core수 만큼 자동으로 설정됨
- worker_connections 1024;
    - worker thread 당 최대 몇 개의 connection을 처리할 것인지  정의
    - 최대 처리량 = worker_processes * worker_connections
- reverse proxy , Load Balancer, Web Cache 서버 등 설정에 따라 다양하게 사용가능
    