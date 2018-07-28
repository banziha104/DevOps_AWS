# CI/CD (지속적인 통학과 배포)



### Jenkins

- 파이프라인을 통해 **지속적인 통합과 전달(CI & CD)** 환경구축을 위한 툴
- 거의 대부분의 언어를 지원
- CI/CD 툴 중 가장 많은 thrid-party 지원
- 강력한 빌드, 테스트, 배포를 통합적으로 지원
- 파이프라인 : 코드상에서도 CI / CD 제어 가능 


### 젠킨스 설치 및 구동

1. 깃 레파지토리 생성 
2. Jenkins가 구축될 EC2 instance 생성 (젠킨스는 8080을 이용하기 때문에 8080 포트를 열음)
3. 젠킨스 설치
    - sudo ssh -i ~/Desktop/ec2_test.pem ec2-user@{jenkins 인스턴스 DNS 주소} 
    - sudo su
    - yum -y update
    - yum install -y java-1.8.0 (젠킨스가 자바로 구동되기 떄문에 설치필요!)
    - wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo 
    - rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
    - yum install -y jenkins
 
4. git 설치 : yum install -y git
5. 젠킨스 구동 :  service jenkins start
6. Jenkins가 구동 됨에 따라 8080포트가 열려있는 지(제대로 실행되고 있는 지) 확인 : netstat -na | grep 8080
7. 웹에서 한번더 확인


### 젠킨스 설정 및 실행

1. 패스워드 위치 확인

2. cat 패스워드위치 (예 : cat /var/lib/jenkins/secrets/initialAdminPassword ) 로 확인

3. 접속

4. 추천 플러그인 설치

5. Admin User 설정

6. URL에 8080포트인지 확인

7. 메인화면

8. 새작 만들기

9. FreeStyle Project 클릭 ( pipeline ...? 은 따로공부)

10. 프로젝트 설정

11. General -> Github project 


12. 소스코드관리 -> Git : Crendential Add 클


13. Credential Provider 이미지

14. 빌드 유발 (그냥 언제시작할래...) -> GitHub hook trigger for GITScm polling
    
15. 깃헙 서비스 등록

16. Jenkins Hook 등록 : {ec2 url}8080/github-webhook/

17. Webhooks 설정 
    - Jenkins 훅과 같은 url 
    - content-type ->  application/json 
    
18. 어느 이벤트에 반응할지 (Which events would you like to trigger this webhook?)
    - Just the push event : 푸쉬이벤트
    - 아무거나왔을때
    - let me select individuals events : 내가 원하는 것 암거나.. fork 등등 많음

19. 빌드환경 -> 설정안함


20. 테스트 실행 : 푸쉬 해봄

21. 실행되었는지 확인

22. 내용확인 : cd /var/lib/jenkins/workspace 로 이동

### 젠킨스 플러그인 설치 및 설정

1. 젠킨스관리 -> 플러그인

2. publish over ssh 설

3. 재 로그인

4. 젠킨스 관리 -> 시스템 설정 -> Publsh Over SSH 설정 

5. cat 명령어를 이용해 내용 받아오기 (cat aws_test.pem) : Begin으로 시작해 END로 끝

6. aws 가져오기 

7. Publish Over SSH 설정

- Path to key : ssh key가 위치한 경로
- Key : ssh key 본문 입력 (Path to key가 우선순위가 높음)
- Disable exec : shell script 실행을 막기 위해 사용
- SSH Servers 
    - Name : 서버이름
    - Host Name : 배포할 인스턴스의 Public ip 
    - Username : ssh 로그인 시 접속할 계정의 ID(ec2-user) : ec2 콘솔에서 cd /home 했을떄 있는 계
    - Remote Directory : ssh로 접속시 맨 처음 들어 갈 디렉토리의 경로
    
8. item -> 구성 클릭

9. 맨아래 빌드 후 조치 -> send build artifacts over SSH 클릭 : 이건 빌드후에 .war, .html 이 됬던 보낼수있음 
    - Source files : 무엇을 보낼지 *.apk 같은 것도 가능
    
10. 메인으로 돌아와 시계 클

11. Remote directory와 Exec command 실행

Exec command
기존에 운영되고 있던 프로젝트 삭제

sudo rm -rf /usr/share/nginx/html/
sudo mv ./Fastcampus-web-deploy /usr/share/nginx/html/
-
Fastcampus-web-deploy
- -
배포된 프로젝트 코드를 Nginx root directory
-
로 이동

    
### 시크릿박스 알아보기!!

