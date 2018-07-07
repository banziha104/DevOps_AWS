# Docker

- amazon-linux-extras install docker

- service docker start : 도커 데몬 실행

- docker pull nginx:latest : 

- docker run -d -p 8080:80 --name Nginx nginx:latest

- docker ps -a :

- 인바운드 규칙 변경


### 도커 단점

- 메인 OS가 윈도우인 경우, 컨테이너의 OS도 윈도우여야함



# 용어

- Docker 
    - 컨테이너 기반의 오픈소스 가상화 플랫폼
    - 다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순화 할 수 있음
    - OS위에 또 다른 OS를 올려야 하는 비효율적인 가상 머신의 단점을 극복하기 위해 나온 가상화 어플리케이션
    
- Docker 컨테이너
    - 도커엔진위에서 동작하는 가상화된 OS 어플리케이션
    - VM처럼 하드웨어 가상화가 아닌 OS만을 가항화하여 Host OS와 커널 등 겹치는 기능을 공유
    - 컨테이너 내에서 동작할 어플리케이션에 필요한 바니어리만 패키징되어 가볍고 속도가 빠름
    

    
    