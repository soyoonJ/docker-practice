npm init -y
npm i express

index.js에서 간단한 서버 구축

# Dockerfile 작성

빈번하게 변경되는 파일일수록 나중에 작성
ex) package.json 작성 -> index.js 작성

npm install < npm ci 사용 권장

- npm install은 설치할 당시 최신 버전이 나왔다면 최신 버전으로 설치함
- npm ci는 package-lock.json에 명시되어 있는 버전으로 설치 가능

COPY package.json package-lock.json ./
package.json과 package-lock.json을 ./로 복사

ENTRYPOINT [ "node", "index.js" ]
node를 실행할거고, index.js를 실행해라

# Docker Build

docker build -f Dockerfile -t docker-practice .
-f : 어떤 Dockerfile을 사용할 것인지 명시
-t : docker image에 이름 부여 가능
. : 현재 경로

docker images
로컬 머신에 만들어진 이미지들을 확인할 수 있음

docker run -d -p 8080:8080 docker-practice  
-d : detached
-p : port 지정 (호스트 머신에 있는 포트와 컨테이너에 있는 포트를 연결)

docker ps
현재 실행 중인 컨테이너들의 리스트 확인 가능

localhost:8080 접속하면 잘 동작하는 것 확인 가능

docker logs [container id]
로그나 다양한 정보를 확인하고 싶을 때
컨테이너에서 발생하고 있는 터미널 메시지 확인 가능

# Container Registry에 생성한 Image 올리기

Docker Hub 계정 가입 후 repository 생성
https://hub.docker.com/repository/docker/judydobrain/docker-practice/general

docker tag docker-practice:latest judydobrain/docker-practice:latest
이미지 이름이 repository 이름과 매칭되어야 함
(docker push judydobrain/docker-practice:tagname - 홈페이지에 나온 명령어)

docker login
도커 로그인 명령

docker push judydobrain/docker-practice:tagname
도커 push
