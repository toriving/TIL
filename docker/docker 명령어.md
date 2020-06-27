# Docker 기본 명령어

Created: Jun 28, 2020 12:30 AM
Tags: Docker

docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]  

|옵션|설명|
|------|---|
|-d|detached mode 흔히 말하는 백그라운드 모드|
|-p|호스트와 컨테이너의 포트를 연결 (포워딩)|
|-v|호스트와 컨테이너의 디렉토리를 연결 (마운트)|
|-e|컨테이너 내에서 사용할 환경변수 설정|
|-it|컨테이너 이름 설정|
|--name|프로세스 종료시 컨테이너 자동 제거|
|--rm|-i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션|
|--link|컨테이너 연결 [컨테이너명:별칭]|

**docker version** : docker 버전  
-> docker --version (간략)  

**docker info**  : docker 상세 설치 정보  

**docker images** : 도커에 설치 되어 있는 image를 출력

**docker ps -a** : 도커 내부에 존재하는 모든 컨테이너를 출력

**docker run mycontainer** : mycontainer 실행   
→ local에서 찾고 존재하지 않으면 hub에서 pull 해옴  
→ create + start + attach 를 한번에 하는 것과 같음  
  
**docker pull [OPTIONS] NAME[:TAG|@DIGEST]** : 이미지 다운  
→ docker pull ubuntu:14.04   

**docker rmi [OPTIONS] IMAGE [IMAGE...]** : 이미지 삭제  
→ docker rmi ${IMAGE_ID}  

**docker create mycontainer** : mycontainer container 생성 (실행 X)  
→ docker create -i -t --name (내가 설정하려는 컨테이너 이름) (이미지 이름)  

**docker start mycontainer** : 생성한 컨테이너 실행  
-> docker start centos

**docker rename ${기존} ${변경}** : container 이름 변경  
-> docker rename centos danny

**docker attach mycontainer** : mycontainer 컨테이너 접속  
-> docker attach danny

**ocker stop [OPTIONS] CONTAINER [CONTATINER...]** : 중지  
→ docker stop ${ID}  
→ rm 과는 다르게 stop을 한 후 다시 start 하면 전에 했던 작업을 이어서 할 수 있음  

**docker rm [OPTIONS] CONTAINER [CONTATINER...]** : 제거  
→ docker rm (-f) ${ID}  
→ 실행하고 작업했던 모든 내용이 삭제됨  

**docker container prune** : 모든 컨테이너 삭제  
→ docker stop $(docker ps -a -q) \ docker rm $(docker ps -a -q)  
 
**docker logs [OPTIONS] CONTAINER** : 컨테이너 로그 보기  
→ docker logs ${CONTAINER_ID}  
→ docker logs --tail 10 ${CONTAINER_ID}  
→ docker logs -f ${CONTAINER_ID}

**docker exec [OPTIONS] CONTAINER COMMAND [ARG...]** : 컨테이너 명령어 실행하기  
(run은 새로 컨테이너를 만들어서 실행 / exec는 실행중인 컨테이너에 명령)