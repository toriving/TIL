# Dockerfile 기본 명령어

```
# 1. ubuntu 설치 (패키지 업데이트 + 만든사람 표시)
FROM       ubuntu:16.04
MAINTAINER subicura@subicura.com
RUN        apt-get -y update

# 2. ruby 설치
RUN apt-get -y install ruby
RUN gem install bundler

# 3. 소스 복사
COPY . /usr/src/app

# 4. Gem 패키지 설치 (실행 디렉토리 설정)
WORKDIR /usr/src/app
RUN     bundle install

# 5. Sinatra 서버 실행 (Listen 포트 정의)
EXPOSE 4567
CMD    bundle exec ruby app.rb -o 0.0.0.0
```

**FROM** 
: 베이스 이미지를 지정 
```
FROM <image>:<tag>  
FROM ubuntu:16.04  
```

**MAINTAINER**  
: Dockerfile을 관리하는 사람의 이름 또는 이메일 정보 (빌드 영향 X)  
```
MAINTAINER <name>
MAINTAINER subicura@subicura.com
```

**COPY**  
: 파일이나 디렉토리를 이미지로 복사. target 디렉토리가 없다면 자동 생성  
```
COPY <src>... <dest>
COPY . /usr/src/app
```

**ADD**  
: COPY 명령어와 유사.   
src에 파일 대신 URL 입력 가능.   
src에 압축 파일을 입력하는 경우 자동으로 압축 해제하면서 복사  
```
ADD <src>... <dest>  
ADD . /usr/src/app  
```

**RUN**  
: 명령어 실행. (내부적으로 `/bin/sh -c` 뒤에 명령어 실행)  
```
RUN <command>  
RUN ["executable", "param1", "param2"]  
RUN bundle install  
```
 
**CMD**  
: 도커 컨테이너가 실행되었을 때 실행되는 명령어를 정의  
빌드 할 때는 실행 X  
여러 개의 `CMD` 가 존재 할 경우 가장 마지막 `CMD` 만 실행.  
한꺼번에 여러 개의 프로그램을 실행하고 싶은 경우에는 run.sh 파일을 작성하여 데몬을 실행하거나,  
supervisord나 forego와 같은 여러 개의 프로그램을 실행하는 프로그램을 사용  
```
CMD ["executable","param1","param2"]
CMD command param1 param2
CMD bundle exec ruby app.rb
```

**WORKDIR**
: RUN, CMD, ADD, COPY 등이 이루어질 기본 디렉토리 설정.  
각 명령어의 현재 디렉토리는 한줄 한줄 마다 초기화 되기 때문에 `RUN cd /path`를 하더라도 다음 명령어에선 다시 위치가 초기화 됨.  
같은 디렉토리에서 계속 작업하기 위해서 `WORKDIR`을 사용함
```
WORKDIR /path/to/workdir
```

**EXPOSE**  
: 도커 컨테이너가 실행되었을 떄 요청을 기다리고 있는 포트를 지정. (여러개 가능)  
```
EXPOSE <port> [<port>...]
EXPOSE 4567
```

**VOLUME**  
: 컨테이너 외부에 파일시스템을 마운트 할 때 사용.   
반드시 지정하지 않아도 마운트 할 수 있지만, 기본적으로 지정하는 것이 좋음.  
```
VOLUME ["/data"]
```

**ENV**  
: 컨테이너에서 사용할 환경변수 지정.  
컨테이너를 실행할 때 `-e` 옵션을 사용하면 기존 값을 오버라이딩 하게 됨.  
```
ENV <key> <value>
ENV <key>=<value> ...
ENV DB_URL mysql
```

**Build**  
: 도커 이미지 빌드.  

```
docker build [OPTIONS] PATH | URL | -
생성할 이미지 이름을 지정하기 위한 -t(--tag) 옵션만 알면 빌드가 가능합니다.

Dockerfile을 만든 디렉토리로 이동하여 다음 명령어를 입력합니다.

docker build -t app .
```

## Reference
- https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html
