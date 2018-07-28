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
    
- Load Balancer : 동시 접속자를 분배해줌, 
    - Health-Check
        -  각 인스턴스들에게 주기적으로 정삭적으로 작동하고 있는 지 물어본다.
        - 확인 요청을 보냈을때 200번대 HTTP status code를 주면 정상
        - 그외의 HTTP status code를 받으면 장애 상태라 판단하고 정상적인 인스턴스에게만 요청을 전달한다.
        
- AWS ELB 
    - 서버 트래픽 분산
    - 동시 접속 최대 사용자 수가 가늠이 안될 때
    - 마케팅 진행시
    
- Scale Out : 추가서버를 붙임 (서버 추가)
- Scale Up : 사양을 늘림 (사양 추가, Ai, Bid Data 등 고성능 머신이 필요한 경우)

- Auto Scaling Group : 특정 조건에 해당되면 자동으로 EC2 생성, 운영