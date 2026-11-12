# 내 컴퓨터에 개발자용 '작업실' 꾸미기

## 1. 프로젝트 개요

이 저장소는 터미널 기본 조작, 권한 변경, Docker 설치 및 컨테이너 실행,
Dockerfile 기반 커스텀 이미지 제작, 포트 매핑, Docker 볼륨, Git/GitHub 연동을
실습하고 그 결과를 기록하기 위한 미션 저장소입니다.

**미션 제목:** 내 컴퓨터에 개발자용 '작업실' 꾸미기

---

## 2. 실행 환경

**OS / 쉘 / 터미널:**
- OS: Windows 10 (빌드 26300.9974)
- 쉘: Git Bash (MINGW64)
- 터미널: Git Bash

```bash
$ uname -a
MINGW64_NT-10.0-26300 GNIA-C202-B01 3.6.10-5a1665c8.x86_64 2026-09-28 10:40 UTC x86_64 Msys

$ docker --version
Docker version 29.9.3, build a82e528

$ git --version
git version 2.56.0.windows.4


```
$ ./permission_test.sh
```
## 3. 파일 권한 실습

권한 실습 성공

$ chmod 644 permission_test.sh

$ ls -l permission_test.sh
- rw-r--r-- 1 dabin52171136 1049089 48 Nov 9 12:41 permission_test.sh*

$ chmod 755 permission_test.sh

$ ls -l permission_test.sh
-rwxr-xr-x 1 dabin52171136 1049089 48 Nov 9 12:41 permission_test.sh*

$ ./permission_test.sh
권한 실습 성공

4. Docker 컨테이너 실행 실습

- docker run -d --name web-test -p 8080:80 nginx
- http://localhost:8080
- docker ps
CONTAINER ID   IMAGE   COMMAND                  CREATED         STATUS         PORTS                  NAMES
b31a3bc12c13   nginx   "/docker-entrypoint…"   13 seconds ago  Up 12 seconds  0.0.0.0:8080->80/tcp   web-test

docker stop web-test
docker rm web-test

docker run --rm hello-world

5. Dockerfile 기반 커스텀 이미지 제작

5-1. Dockerfile 작성

FROM nginx:stable

COPY ./html /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

5-2. HTML 파일 작성

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>개발자 작업실</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }
        .container {
            background: white;
            padding: 50px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }
        h1 { color: #333; }
        p { color: #666; line-height: 1.8; }
    </style>
</head>
<body>
    <div class="container">
        <h1>🚀 개발자 작업실</h1> 
   <p>Docker를 활용한 커스텀 개발 환경이 준비되었습니다!</p>
        <p>✅ Dockerfile 기반 이미지 빌드 완료</p>
        <p>✅ 커스텀 nginx 컨테이너 실행 중</p>
    </div>
</body>
</html>

5-3. 이미지 빌드 및 컨테이너 실행

$ docker build -t my-nginx:local .
[+] Building 2.3s (6/6) FINISHED
 => [internal] load build definition from Dockerfile
 => [base 1/3] FROM nginx:stable
 => [base 2/3] COPY ./html /usr/share/nginx/html
 => exporting to image
 => naming to docker.io/library/my-nginx:local

$ docker images
REPOSITORY   TAG     IMAGE ID       CREATED        SIZE
my-nginx     local   abc123def456   2 minutes ago  187MB
nginx        stable  1234567890ab   2 weeks ago    187MB

$ docker run -d --name my-web -p 8080:80 my-nginx:local
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6

6. 프로젝트 파일 구조

my-docker-project/
├── Dockerfile
├── html/
│   └── index.html
├── permission_test.sh
└── README.md

7. 학습 성과

✅ Docker 이미지 빌드 및 실행
✅ Dockerfile 작성 및 커스텀 이미지 제작
✅ 포트 매핑을 통한 로컬 웹 서버 접속
✅ 파일 권한 관리 (chmod)
✅ Git을 통한 프로젝트 버전 관리

---
