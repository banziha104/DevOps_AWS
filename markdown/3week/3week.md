### Node.js 설치

- sudo ssh -i ~/Desktop/ec2_test.pem ec2-user@{접속할 WAS 인스턴스 DNS 주소} ↵ sudo su ↵
- curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
- yum install -y nodejs
- node -v
- npm -v


### Git 설치 및 가져오기

- yum install -y git
- git clone -b v1 https://github.com/owen1025/Fastcampus-api-deploy.git : v1 브랜치를 가져옮
- ls -al
- cd Fastcampus-api-deploy/


### Pm2로 백그라운드로 구동하기

- npm install -g pm2
- npm install
- pm2 start Fastcampus-api-deploy/bin/www --name WAS 
- pm2 list
- pm2 show WAS