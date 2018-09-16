# Docker #

## Docker 자주 사용하는 명령어 모음 ##

- search : 이미지 검색
- 형식 : docker search {검색한 이미지명}

```bash
$ sudo docker search ubuntu // 우분투 이미지 검색
```

- pull : 이미지 받아오기
- 형식 : docker pull {이미지 이름}:{태그}

```bash
$ sudo docker pull ubuntu:latest // 최신 우분투 이미지를 받아
```

- images : 현재 받은 이미지 출력
- 형식 : docker images {이미지명}?

```bash
$ sudo docker images
$ sudo docker images ubuntu //우분투 이미지 출력 여러버전이 있다면 전부 
```

- run : 이미지를 작동 시킴 이미지에서 새 컨테이너 생성
- 형식 : docker run {옵션} {이미지 이름} {실행할 파일}
	- -i : ??
	- -t : 해당 컨테이너 쉘로 바로 들어감
	- --name : 해당 컨테이너의 이름 설정
	- --link : 다른 컨테이너와 연결해 사용 가능
	- -w : working directory 독커 내에서의 기본 디렉토
	- -p : 컨테이너의 포트와 실제 포트와 맵핑 시킬 수 있음

```bash
docker run \
	-it
    --name nodeapp \
    -v "$(pwd)":/data \
    --link mongo:mongo \
    -w /data/hw3-2and3-3/blog \
    -p 8082:8082 \
    -d node node app.js

```


- ps : 모든 컨테이너 목록을 출력
	- -a : 정지된 컨테이너 목록도 출력

- start : 해당 컨테이너를 실행
- restart : 해당 컨테이너를 재실행함
- attach : 실행중인 컨테이너 내부 쉘로 접속 
	
	- Ctrl+P, Ctrl+Q 를 사용해 해당 컨테이너에서 빠져 나올수 있음

- exec : 해당 컨테이너로 명령을 보냄 결과도 보여
- rm : 컨테이너 삭제 (컨테이너다. 이미지가 아니라)
- rmi : 이미지 삭제

## Dockerfile 만들기 ##
컨테이너 빌드를 위한 파일 이다.
명령어나 기타 설정을 통해 기본 이미지를 병합하거나 커스터마이즈 할 수 있다.

## 사용한 명령어 ##
- rename : 컨테이너 명을 변경 한다

```bash
$ docker rename {원래 이름} {변경할 이름}
//docker rename lonely wooesidari
```
- 예시와 같이 작성하면 컨테이너 명이 변경된다.

- exec : docker 내부로 명령어를 전달 해줌 결과 값을 볼 수 있다.
 
- inspect : docker container 의 정보를 json 형태로 보여줌

```bash
$ docker inspect {컨테이너명}
```

## Docker sudo 없이 실행 하기 ##
- 해당 계정을 docker 그룹에 등록하면 됨
```bash
sudo usermod -aG docker $USER
```
- 그룹 확인은 `groups` 을 치면 등록된 그룹을 확인 할수 있음
- 위 명령어보다 /etc/group 문서를 확인해보는 것이 더 확실함
- 위에 문서에 있는데 그룹이 안됬으면 재 로그인
- gpasswd : 그룹 관리 하는 명령어
	- -a {계정명} : 특정 그룹에 서로운 맴버를 추가
```bash
$ gpasswd -a zezz wheel
//zezz 사용자를 wheel 그룹에 설정rkdg
```

[그룹명령어 참조](http://webdir.tistory.com/134)

## 주로 이용 하는 run ##
```bash
sudo docker run -it -d --name markdown_app -p 80:80 -v /home/rkdgusrnrlrl/docker/node/markdown_generator:/data -w /data  node bash
```
