# Deployment


###  In-place Deployment ( 직접배포 )
- 중단 배포
- 정기 점검
- AWS Codedeploy를 활용하여 무중단 배포가 가능
    

### Blue-green Deployment 

> 두개의 **동일한 환경** 인 블루 환경과 그린 환경을 이용해 무중단 배포

- 블루 환경 : 운영 중인 환경
- 그린 환경 : 업데이트 될 환경
- 작동 방식
    1. 새로운 소프트웨어, 환경 Build -> Deployment
    2. 실제 운영 환경에서 테스트 진행
    3. 블루환경을 삭제후 그린환경 영역으로 운영환경 변경
    4. Blue-green 영역을 Switching 하여 트랜잭션 보장 가능
    
    
### Docker

1. git clone
2. 프로젝트 이동 : cd project
3. vim Dockerfile : 도커 파일 작송
4. docker build 실행
