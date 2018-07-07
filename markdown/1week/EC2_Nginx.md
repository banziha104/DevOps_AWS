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



### 용어 

- 가상서버 : 물리 머신 위에 독립적 OS 실행이 가능한 논리적인 가상의 서비스를 생성하여 실행
- Amazon Linux2 
    - AWS에서 제공하는 차세대 Linux 운영 체제
    - Amazon Linux Extras 리포지토리를 이용해 최신 서비스를 받을 수 있음
    - Container 환경에 최적화 된 OS (*)
    - 가벼운 OS는 아님
    
- AWS AMI : Amazon Machine Image(AMI), 
    - 윈도우 CD,iSO와 가은 개념
    - 서버 인스턴스의 기반이 되는 이미지
    - Amazon에서 제공하는 빅데이터, 웹서비스 등 각 기능별로 빌드한 이미지를 사용하거나 다른 사람이 공유하는 이미지도 가능
    
- SSH 클라이언트 
    - SSH은 다른 컴퓨터에 접속하나 원격 시스템에서 명령을 실행할 수 있는 프로토콜 및 클라이언트 의미
    - 대부분의 리눅스 배포판에선 기본적으로 설치되어있음
    - 22번 포트
    - -i 옵션으로 비밀번호가 아닌 SSH key로 접속
    
- SSH Key
    - 비밀번호보다 높은 수준의 보안을 필요할 때 사용
    - SSH 서버에 저장된 Public Key와 사용자의 Private Key를 비교하여 접속

- sudo : 관리자 권한으로 실행하고 싶을때 사용

- 웹서버 : 
    - HTTP 요청을 받고 응답하는 역할을 함
    - HTTP transaction을 처리하고 정적인 파일을 요청한 대상에게 보내준다
    - Application logic을 직접 처리할 수 없어 WAS 와 같이 사용함
    
- Nginx
    - 아파치의 한계를 극복하기 위해 나옴
    - 동시접속 1만개 당 평균 메모리 점유율 2.5mb
    
- WAS 
    - 동적인 데이터를 생성하여 응답하는 서버
    - 어플리케이션 로직을 직접 실행하는 서버
    - 톰캣, WSGI,jBoss 등

- 서버 프론트 : Web Server 
- 서버 백엔드 : WAS

- DNS : 도메인 네임 서비스
    - 모든 디바이스는 IP로 통신
    - IP를 외우기 귀찮으니 IP와 URL을 매핑하여 전화번호부 같은 역할을 함.
    
- Port : 
    - TCP/IP 로 접속시 마지막 종단점
    - 클라이언트 실행 시 동적으로 Port 번호가 부여
    - 해당 인스턴스에서 실행되는 클라이언트의 구분을 위해 사용
    - 일반적으로 SSH(22), HTTP(80번) , WAS(8080)을 부여
    - URL 접속시 80번 포트를 사용 (생략가능)
    
### 리눅스 별 차이 

   



