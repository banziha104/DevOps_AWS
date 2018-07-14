
# Git

### git을 통한 배포

```shell
yum install -y git
cd /usr/share/nginx/html 
git clone https://github.com/owen1025/Fastcampus-web-deploy.git
// http://ec2-52-79-228-106.ap-northeast-2.compute.amazonaws.com/Fatcampus-web-deploy/ 로 접속
```

- 소스 코드 관리를 위한 분산형 버전 관리 시스템
    - 소스 코드를 버전 별로 관리하며 예전버전으로 rollback 이나 협업을 하며 코드를 합치기 쉬워짐
    - 브랜치 별로 커밋/머지 된 코드를 분리하여 운영 개발 환영게 각각 배포할 수 있다.
    
- Git 브랜치 예시
    - develop : 각 개인의 코드를 합치기 위한 테스트 코드 버전 관리 브랜치. 개인 테스트가 마친후 커밋후 관리지가 머지하는 것을 원칙
    - hotfix : 긴급 수정 코드 머지를 위한 브랜치. 관리자가 부재시 해당 모듈/서비스 담당자가 머지하는것을 허용
    - stage : 개발 환경에 배포를 위한 develop/hotfix 브랜치에 머지된 코드가 있을 경우 테스트 환경에 자동 배포
    - production : stage 브랜치에 머지된 코드를 확인, 테스트 환경에서 미리 정의된 테스트 시나로이를 전부 통과하면 관리자에게 Slack으로 알림, hotfix인 경우, 알림 없이 운영 환경에 자동배포