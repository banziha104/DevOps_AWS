# ELB 

- AWS에서 제공하는 L4 스취 기능을 제공하는 로드 밸런싱 서비스
- ELB가 받은 요청을 해당하는 EC2, 서비스 그룹 등 다양하게 전달 할 수 있음
- 너무 많은 요청을 처리하고 있거나 정상적으로 동작하지 않는 서버에는 요청을 보내지 않음

- 로드밸런서 종류
    - 클래식 : 미니멀 한 기능을 제공
    
    - Application LB : 복수의 어플리케이션을 1개의 로드밸런서로 처리(서비스 단위로 잘게 쪼게져있을 때, 서비스 별로 확장가능)


## ELB 확인
- 로드밸런서 정의 및 생성

![1](https://github.com/banziha104/DevOps_AWS/blob/master/img/img2week/1.png)

- 로드 밸런서를 웹서버랑 이어줌 (로드밸런서 프로토콜 80, 인스턴스 프로토콜 80)

![2](https://github.com/banziha104/DevOps_AWS/blob/master/img/img2week/2.png)


- 보안 그룹 할당

![2](https://github.com/banziha104/DevOps_AWS/blob/master/img/img2week/3.png)

- 상태 검사 구성
    - Ping 프로토콜
    - Ping 포트
    - Ping 경로 
    - 응답 시간 초과 : ELB가 헬스체크시 최대 시간
    - 간격 :
    - 비정상 임계값 : 횟수만큼 헬스체크에 실패하면 비정상판단
    - 정상 임계값 : 횟수만큼의 헬스체크에 통과하면 정상판단 


![5](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/5.png)

    
- EC2 인스턴스 추가
    - 교차 영역 로드 밸런싱 활성화 : 트래픽을 분산할건지
    - 연결 드레이닝 활성화 : 존 트래픽이 플로우를 지속하도록 허용할 기간

![6](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/6.png)

    
- 생성

![7](https://github.com/banziha104/DevOps_AWS/blob/master/img/img1week/7.png)


- 인스턴스 상태 확인 
    - OutOfService :  서비스 중이 아님
    - InService : 서비스 중  
    
    
- DNS 확인
