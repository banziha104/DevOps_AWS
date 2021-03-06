# ECS

# ECR (Elastic Container Registry)

- Docker 컨테이너 이미지를 손쉽게 저장, 관리 , 및 배포할 수 있게 해주는 완전관리형 Docker 컨테이너 레지스트리
- AWS ECS와 결합하여 EC2 인스턴스에 컨테이너 배포까지 통합지 

1. ECS 검색

2. ECR 리포지토리 클릭

3. $(aws ecr get-login --no-include-email --region ap-northeast-2)

4. 그대로 복사해서 실행

4. docker build -t web-repo .

5. docker tag web-repo:latest 635345261195.dkr.ecr.ap-northeast-2.amazonaws.com/web-repo:latest

6. docker push 635345261195.dkr.ecr.ap-northeast-2.amazonaws.com/web-repo:latest

<br>

# 클러스터 

> AWS EC2 instance를 하나의 서버처럼 구성하기 위해 클러스터링 진행  

- 몇 대의 인스턴스를 생성할 것인지 (Auto Scaling Group 적용 가능)
- 지시한 인스턴스 별로 ECS-agent 설치
- 컨테이너 배포 스케쥴링 및 서비스 디스커버리 실행
- 여러 대의 EC2가 클러스터링 되어 있으며, 스케쥴링에 의해컨테이너가 구성됨
- 스케쥴러가 임의로 컨테이너의 포트를 부여 하기에 각  EC2의 보 그룹엔 모든 포트를 허용해야함
- 추후에 작업 정의를 통해 사용할 컨테이너 포트의 대역대를 설정할 수 있음


1. 클러스터 클릭

2. Linux 설치 

3. 설정

4. 생성


## 작업 정의

- 어플리케이션을 구성하는 컨테이너를 설명하는 JSON 형식의 텍스트 파일 최대 10개
- 어떤 Docker image를 기반으로 구성할 것인지
- 컨테이너에서 사용할 포트 및 네트워크 설정
- 컨테이너가 사용할 서버 리소스 (CPU,RAM 등) 결정


1. 작업 정의 실행

2. 작업 정의 생성
    - 작업 역할 : 더알아보기
    - 네트워크 모드 : 대부분 브리지를 사용 
        - 브리지 : docker0 bridge 모드, dynamic port mapping
        - 호스트 : Docker daemon이 운영되는 Host 머신의 네트워크 인터페이스를 그대로 사용
        - aws vpc : EC2 instance에 적용하는 탄력적인 네트워크 인터페이스를 컨테이너에 적용(elastic dns / ip), Aws Far Gate 시 사용
        
    - 작업 메모리 : 컨테이너 당 얼마 많은 큼의 메모리를 사용할지
    - 작업 CPU : 컨테이너 당 얼마나 사용할지 (1CPU는 1024 유) 
    
3. 컨테이너 추가 
    - 컨테이너 이름 : 이름
    - 이미지 : docker 이미지
    - 메모리 제한
        - 하드 제한 : 500인 경우, 500mb 넘으면 컨테이너를 꺼뻐림
        - 소프트 제한 : 256인 경우, 최소한 256mb를 차지하겠다라 선언


4. 기타 설정
    - 헬스체크
    - 환경 : 볼륨 등을 설정 가능
   
5. 생성

6. 클러스터 클릭 -> 서비스 -> 생성 

7. 서비스 구성
    - 서비스 이름 : 해당 서비스의 이름
    - 서비스 유형
        - REPLICA : 부하 분산을 위해 해당 갯수만큼의 운영이 가능한 컨테이너 생성
        - DEAMON : 고가용성을 위해 예비 컨테이너의 생성
        - RDS의 multi-AZ와 read replica의 차이와 동일
    - 작업 개수 : 몇개의 컨테이너를 띄지
    - 작업 배치 
        - AZ 균형 분산 : 클러스터링 된 EC2 인스턴스에 고르게 배포
        - AZ 균형 빈팩 : 클러스터링 된 EC2 인스턴스 중 가장 적은 갯수와 메모리를 종합적으로 고려하여 인스턴스에 배포
        - 호스트 당 작업 한 개 : 하나의 인스턴스에 하나의 서비스 배포
        - 빈팩 : 가장 적은 메모리를 사용하는 인스턴스에 배포 
        
        
8. 네트워크 구성

9. 어플리케이션 로드 밸런서 생성
    - WAS 가 80번과 3000번이 다르게 작동함으로 80,3000 둘다 오픈 
    
    - 보안그룹 구성
    
    - 라우팅 구성 
    
    - 대상 구성 : 컨테이너를 띄우고 나서 하면, 해당 컨테이너도 선택가
    
    
10. 로드 밸런서 적용

11. Auto Scaling

12. 서비스 검사


# Container Orchestration

> 컨테이너 배포를 위해 EC2 instance 클러스터링

- ECS-Agent
    - 컨테이너 배포 전략 수행
    - Dynamic port mapping , 서비스 디스커버리 등의 컨테이너 관리 수행을 하는 ecs-agent를 각 인스턴스에 설치


## 팁

> Nginx로 웹서버를 띄울땐, 다음이 표준

- 메모리 512
- 하드 제한 500
- 소프트 제한 256 

