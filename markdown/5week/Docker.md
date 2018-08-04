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
    
 
 
 # 기타 
 
 - nmap : 열려 있는 모든 포트를 볼 수 있음
    - yum install -y nmap 
    - nmap localhost | grep http
