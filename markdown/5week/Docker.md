# Docker 명령어

- docker ps -a docker container : 프로세스 확인
- docker stop web1 : 실행되고 있는 docker container 프로세스 종료, docker run 시 name 옵션으로 지정한 컨테이너 이름으로 종료가능
- docker rm web1 : 컨테이너 삭제 , 컨테이너 삭제시 실행 중이면 삭제 안됨, stop 명령어로 종료 후 삭제
- docker rmi web1 : 이미지 삭제 
- docker run -d -p 8000:80 --name web1 web:latest
    - run : docker image를 기반으로 컨테이너 생성/실행
    - d : 데몬으로 실행
    - p : 포트 매핑(HOST에 8000포트로 들어온 요청을 컨테이너 내 80 포트와 연결)
    — name : 컨테이너 이름 설정
    - web:latest : 해당 이미지를 기반으로 컨테이너 실행
  
- docker pull centos:latest : 이미지를 가져옮 
    - pull : 외부 레포지토리에서 이미지 다운로드, 따로 명시된 레 포지토리가 없다면 dockerhub(https://hub.docker.com) 에서 다운로드
    - centos : 다운로드 할 이미지 이름
    - latest : 다운로드 할 이미지의 버전, latest로 명시하면 가장 최근에 업데이트 된 이미지를 가져옴
    
- docker run -it --name cent centos:latest /bin/bash
    - it : -i, -t 옵션으로 실행
    - i(interactive), -t (Pseudo-tty) : Bash shell 입력 및 출력 가능
    - /bin/bash : centos 이미지 내에 /bin/bash 실행 
    
- docker attach web2 : 컨테이너에 접근함 (/bin/bash 로 접근)
- docker exec -it web2 /bin/bash
    - docker run '-d' 옵션으로 백그라운드로 컨테이너 실행시 bash shell 이 아닌 CMD에 명시된 프로세스가 컨테이너 내에서 foregorund로 실행되고 있어 attach로 shell 실행이 안됨
    - Container가 background로 실행 중일 때 컨테이너 내에 접속하기 위해 exec 옵션을 통해 bash shell 실행
    
- ctrl +d : 컨테이너를 종료하면서 나옮
- ctrl +q, ctrl +p : 컨테이너를 종료하지 않으면서 나옮

 # Dockerfile

> CoreOS나 CentOS 기반으로 해야함

- 순서
    - 어떤 OS를 기반으로 실행될 것인지
    - 필요한 소프트웨어를 해당 OS에 맞는 package manger 등을 통해 다운로드
    - 소스 코드, 설정 파일 다운로드 적용
    - 컨테이너 내에서 소프트웨어 구동 및 Port listen

```dockerfile
# 먼테이너 내에서 기반으로 할 OS
FROM centos:latest 

# 뒤에 오는 명령어 실행, 기반이 되는 컨테이너 OS의 체계에 맞춰실행됨
RUN yum install -y epel-release
RUN yum install -y nginx

# 컨테이너 외부에 있는 파일을 내부로 복사 
# copy{external path(도터파일이 존재하는 위치기준) / internal path(해당 컨테이너)} : 디렉토리 / 파일 복사
# 소스코드, 설정파일 등

# WORKDIR /usr/share/nginx/html FROM centos:latest
# WORKDIR 은 RUN으로 명령어 실행시 기본 Path는 /인 root directory에서 실행됨 RUN yum install -y nginx
# NginX root directory에 소스 코드를 배포하기 위해 /usr/share/nginx/html 경로로 작업
COPY ./ /usr/share/nginx/html/Fastcampus-web-deploy

# HOST와 연결될 포트 번호
# Nginx는 80포트로 통신하기에 외부(host)와 연결하기 위해 80포트 설정
# HOST : Dokcer가 구동되고 있는 환경, 물리 머신, VM, 컨테이너 안이 될 수도 있음
EXPOSE 80


# CMD
# 컨테이너가 start(run) / restart 될 때 명령어 혹은 스크립트를 실행
# Dockerfile내에서 한 번만 사용 가능
# RUN ~~과의 차이점
# CMD ["실행 파일", "매개 변수1", "매개 변수2"]
# daemon off 매개변수를 통해 Nginx를 foreground로 실

CMD ["nginx","-g","daemon off;"]

```

### 포어그라운드 백그라운드

- Foreground
    - 기본적으로 모든 프로세스는 foreground로 실행
    - 키보드로부터 입력을 받아 결과를 직접 스크린으로 출력
    - 한 커맨드가 실행되는 동안 다른 커맨드를 실행할 수 없음
    
- Backgorund
    - 키보드와 연결디지 않는 실행 방식
    - 여러 프로세스를 실행할 수 있는 장점이 있음
    - 프로세스 실행시 명령어 뒤에 & 를 붙히거나 프로세스를 관리하는 daemon에 등록하여 실행
    
- 컨테이너 내에선 Foreground로 실행
    - 컨테이너 내에서 실행할 프로세스는 foreground로
    - 해당 컨테이너를 실행시에는 -d 옵션을 통해 background로 실행
    
- 컨테이너를 Background로 실행하면 docker daemon에 등록되며 컨테이너 내에서  background list에 등록된 프로세스가 있다면 충돌이 발생되어 컨테이너 내에선   foreground로 실행하며, 프로세스느 관리는 docker host에 전담


### 기타 
 
 - nmap : 열려 있는 모든 포트를 볼 수 있음
    - yum install -y nmap 
    - nmap localhost | grep http

- 한 컨테이너는 하나의 서비스만 있는게 좋음 

git clone -b container https:// github.com/owen1025/Fastcampus-api-deploy.git


