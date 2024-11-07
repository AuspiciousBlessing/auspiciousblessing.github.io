---
layout: post
title: Docker Basic
description: About the Docker Basic
date: 2024-10-20 03:00:00 +0900
categories: [Technical Labs]
tags: [LAMP, Linux, Apache, MySQL, PHP, Docker]
pin: false
math: false
mermaid: false
image:
  path: commons/docker.png
  alt: HTTP(Hypertext Transfer Protocol)
---
<!-- categories: [Technical Concepts Summarized, Technical Labs, Technical Terms, Useful Apps To Help With Technology] -->

## Overview
도커에 대한 개념 설명은 Technical-Concepts-Summarized에서 자세히 풀어보려고 합니다. 이 포스팅에서는 실제 명령어와 파일 구성을 통해 도커를 어떻게 사용하는지 알아보려고 합니다. 

도커는 명령어 갯수도 적고 사용하기엔 단순한 프로그램이지만 처음 접했할 때는 개념이 매우 생소하기 때문에 전반적인 이해에 큰 어려움이 있습니다. 컨테이너에 대한 이해가 없는 분들은 개념 설명을 먼저 보고 명령어를 따라하며 익히는 것이 좋습니다. 

도커의 기본 필수 명령부터 점점 진화된 방법까지 순차적으로 알아보겠습니다. 저는 처음부터 모든 옵션을 보는 것보다 필수적인 것부터 순차적으로 공부하는 방법을 선호합니다.


(이번 포스팅은 mattrayner/lamp 이미지와 함께 합니다. mattrayner/lamp는 Docker Hub에서 가져온 LAMP Stack 이미지입니다.)

<br>
## Run the basic command line
```shell
sudo docker run -p "80:80" -v ${PWD}/app:/app -v ${PWD}/mysql:/var/lib/mysql mattrayner/lamp:latest-1804
```
명령어 설명
- <span style="background-color: #424242; padding: 0 5px;">docker run</span>: 새로운 컨테이너를 실행합니다.
- <span style="background-color: #424242; padding: 0 5px;">-p "80:80"</span>: 호스트 시스템의 포트 80을 컨테이너의 포트 80에 매핑합니다.
- <span style="background-color: #424242; padding: 0 5px;">-v ${PWD}/app:/app</span>: 호스트의 app 디렉터리를 컨테이너의 /app 디렉터리로 마운트합니다. 컨테이너의 /app 디렉터리는 Apache Server의 루트 디렉터리 입니다.
- <span style="background-color: #424242; padding: 0 5px;">mattrayner/lamp:latest-1804</span>: 이미지명입니다.


<br>
결과
```shell
Unable to find image 'mattrayner/lamp:latest-1804' locally
latest-1804: Pulling from mattrayner/lamp
c64513b74145: Pull complete 
...
e065bd5bccc8: Pull complete 
Digest: sha256:94f6d3e2ea3391c76325441fdd8b1afff7364b89955bc7a5ff4038fc3dd93a5f
Status: Downloaded newer image for mattrayner/lamp:latest-1804
Updating for PHP 8.0
Replacing CLI php.ini values
Editing APACHE_RUN_GROUP environment variable
Editing phpmyadmin config
Setting up MySQL directories
Allowing Apache/PHP to write to the app
Allowing Apache/PHP to write to MySQL
Editing MySQL config
=> An empty or uninitialized MySQL volume is detected in /var/lib/mysql
=> Installing MySQL ...
=> Done!
=> Waiting for confirmation of MySQL service startup
=> Creating MySQL admin user with random password
ERROR 1133 (42000) at line 1: Can't find any matching row in the user table
=> Done!
========================================================================
You can now connect to this MySQL Server with Uj9hgi1VTXGo

    mysql -uadmin -pUj9hgi1VTXGo -h<host> -P<port>

Please remember to change the above password as soon as possible!
MySQL user 'root' has no password but only allows local connections

enjoy!
========================================================================
Starting supervisord
2024-10-23 18:39:19,013 CRIT Supervisor is running as root.  Privileges were not dropped because no user is specified in the config file.  If you intend to run as root, you can set user=root in the config file to avoid this message.
2024-10-23 18:39:19,013 INFO Included extra file "/etc/supervisor/conf.d/supervisord-apache2.conf" during parsing
2024-10-23 18:39:19,013 INFO Included extra file "/etc/supervisor/conf.d/supervisord-mysqld.conf" during parsing
2024-10-23 18:39:19,015 INFO RPC interface 'supervisor' initialized
2024-10-23 18:39:19,015 CRIT Server 'unix_http_server' running without any HTTP authentication checking
2024-10-23 18:39:19,016 INFO supervisord started with pid 1
2024-10-23 18:39:20,017 INFO spawned: 'apache2' with pid 445
2024-10-23 18:39:20,019 INFO spawned: 'mysqld' with pid 446
2024-10-23 18:39:21,212 INFO success: apache2 entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)
2024-10-23 18:39:21,212 INFO success: mysqld entered RUNNING state, process has stayed up for > than 1 seconds (startsecs)
```

이 로그에서 알 수 있는 주요한 정보들
1. 이미지 다운로드 및 설치 완료:
Docker는 mattrayner/lamp:latest-1804 이미지를 로컬에서 찾을 수 없었기 때문에, Docker Hub에서 이미지를 가져와서 설치했습니다.
모든 레이어가 성공적으로 다운로드되어 LAMP 스택이 준비되었습니다.

1. MySQL 설치 및 초기화:
MySQL이 설치되고, /var/lib/mysql에 비어 있거나 초기화되지 않은 MySQL 볼륨이 감지되었습니다. 이를 통해 MySQL이 새로 설치되었음을 알 수 있습니다.
MySQL 서버가 시작된 후, 임의의 비밀번호로 MySQL의 admin 사용자가 생성되었습니다. 이 비밀번호는 Uj9hgi1VTXGo이며, MySQL 서버에 root로 접속할 수 있습니다.
root 계정에는 비밀번호가 설정되어 있지 않지만, 로컬에서만 접속 가능하도록 설정되어 있습니다.

1. MySQL 오류 발생:
MySQL 초기화 과정 중 ERROR 1133 (42000): Can't find any matching row in the user table라는 오류가 발생했습니다. 이는 MySQL user 테이블에서 사용자를 찾을 수 없다는 오류입니다. 이 오류가 특정 설정이나 사용자 생성에 영향을 미칠 수 있으므로, 후속 조치로 사용자 계정과 권한 설정을 확인해야 할 수 있습니다.

1. Supervisor 프로세스 관리:
Supervisor는 Apache와 MySQL 프로세스를 관리하고 있으며, 성공적으로 Apache와 MySQL 프로세스를 실행했습니다. 두 서비스 모두 실행되고 있으며, RUNNING 상태에 진입했습니다.
Supervisor는 기본적으로 root 권한으로 실행되고 있으며, 설정 파일에서 사용자 설정이 정의되지 않았기 때문에 이에 대한 경고 메시지가 나타나고 있습니다.

1. 서비스 실행 상태:
apache2와 mysqld가 각각 RUNNING 상태에 있으며, 1초 이상 실행된 후 성공적으로 서비스가 유지되고 있음을 알 수 있습니다.

<br>
## Options that work well together
```shell
sudo docker run -p "80:80" --name lamp -d -v ${PWD}/app:/app -v ${PWD}/mysql:/var/lib/mysql mattrayner/lamp:latest-1804
```
명령어 설명
- <span style="background-color: #424242; padding: 0 5px;">---name lamp</span>: 도커는 컨테이너를 만들면 추후에 접근하기 쉽도록 임의의 이름을 붙혀줍니다. 하지만 그 이름이 우리가 쉽게 유추할 수 없는 이름입니다. 예를 들면 eager_fermat 같은 이름이 생성됩니다. 따라서 우리가 직접 이름을 붙혀줍니다. -가 두개인 것을 유의하세요.

- <span style="background-color: #424242; padding: 0 5px;">-d</span>: 도커를 데몬으로 실행시킨다는 의미입니다. 도커를 데몬으로 실행시키지 않으면 쉘이 잠겨 있기 때문에 우리는 쉘에서 아무것도 할 수 없습니다. 따라서 데몬으로 실행합니다.

실습을 위해 두가지 명령을 중간에 사용해보겠습니다.

1. 컨테이너의 상태 보기
```shell
sudo docker ps -a
```
명령어 설명
- <span style="background-color: #424242; padding: 0 5px;">docker ps</span>: proccess status의 약어로 컨테이너들의 상태를 보여줍니다.
- <span style="background-color: #424242; padding: 0 5px;">a</span>: 이 옵션이 없으면 실행중인 컨테이너만 보여줍니다. 존재하지만 실쟁중이지 않은 컨테이너까지 모두 보려면 이 옵션을 붙혀줍니다.

    결과
    
    위에서 언급한 것처럼 임의의 이름 eager_fermat이 붙혀진 것을 볼 수 있습니다. 첫번째 명령으로 쉘이 잠겨 Ctrl+C로 실행을 중단했기 때문에 STATUS가 Exited인 것을 볼 수 있습니다.
```shell
CONTAINER ID   IMAGE                         COMMAND     CREATED          STATUS                      PORTS     NAMES
21990a4c72ab   mattrayner/lamp:latest-1804   "/run.sh"   35 minutes ago   Exited (0) 10 minutes ago             eager_fermat
```

2. 현재 만들어진 컨테이너 지우기
아래 명령을 보면 왜 name이 중요한지 알 수 있을 것입니다. 컨테이너ID로도 컨트롤 할 수 있지만 이걸 일일이 오타없이 치기란 쉽지 않습니다.
```shell
sudo docker rm 21990a4c72ab
or
sudo docker rm eager_fermat
```

3. 다시 옵션을 넣고 실행시켜보면 이름이 쉽게 컨트롤할 수 있는 이름인 lamp로 바뀐 것을 확인할 수 있습니다. 
```shell
ab83@auspiciousbleesing:~/webDev$ sudo docker run -p "80:80" --name lamp -d -v ${PWD}/app:/app -v ${PWD}/mysql:/var/lib/mysql mattrayner/lamp:latest-1804
4f79df739d7dcf43a66fdd50229f7226e32fdac058931b50807da57164655d08
ab83@auspiciousbleesing:~/webDev$ sudo docker ps
CONTAINER ID   IMAGE                         COMMAND     CREATED         STATUS         PORTS                                         NAMES
4f79df739d7d   mattrayner/lamp:latest-1804   "/run.sh"   7 seconds ago   Up 6 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp, 3306/tcp   lamp
```

<br>
## Docker's first evolution, the Dockerfile
Docker가 처음 출시되었을 때는 Dockerfile을 기본적으로 지원하지 않았습니다. Docker는 2013년에 처음 공개되었고, 그 당시에는 Docker 이미지를 만들기 위해 기존의 컨테이너를 수동으로 설정한 후 그 상태를 **커밋(commit)**하는 방식으로 이미지를 생성해야 했습니다. 즉, 초기에는 컨테이너 내부에서 직접 작업하고, 그 결과를 이미지로 저장하는 과정이 필요했습니다.

Dockerfile은 나중에 Docker 0.7 버전(2013년 말)에 도입되었습니다. Dockerfile은 이미지 빌드 프로세스를 자동화하고, 더 일관된 이미지 생성을 가능하게 하는 방식으로 큰 인기를 얻었습니다. Dockerfile을 사용하면 특정 명령어들을 정의하여, 컨테이너 이미지를 어떻게 빌드할지 자동으로 구성할 수 있습니다. 이 변화는 개발자들이 이미지를 좀 더 쉽게 정의하고 재현 가능하게 만드는 데 큰 도움을 주었습니다.

### Using Dockerfile
이 방법을 사용해도 위와 동일한 결과를 보여줍니다.

1. Dockerfile 파일명의 Dockerfile 생성
    ```dockerfile
    # 베이스 이미지로 LAMP 스택 사용
    FROM mattrayner/lamp:latest-1804

    # 볼륨 지정
    VOLUME ["/app", "/var/lib/mysql"]

    # Apache 실행
    CMD ["/run.sh"]
    ```

2. Dockerfile 빌드
    ```shell
    docker build -t my-lamp-1804:v1.0.0 .
    docker build -t my-lamp-1804 .
    ```
    명령어 설명
    - **-t**는 **--tag**의 약어로, 빌드된 Docker 이미지에 이름과 태그를 지정할 수 있게 해줍니다.
    - 태그는 선택 사항으로, 미기재시 latest 태그가 붙으며, 명시적으로 다른 버전을 지정할 때 사용합니다.

    <br>
    2.1. 빌드된 이미지 확인

    아까 Docker Hub에서 다운받은 mattrayner/lamp와 직접 만든 my-lamp-1804이미지를 볼 수 있습니다.
    ```shell
    REPOSITORY        TAG                IMAGE ID       CREATED       SIZE
    mattrayner/lamp   latest-1804        2d9935d1db98   3 years ago   931MB
    my-lamp-1804      latest             5f6780a10683   3 years ago   931MB
    my-lamp-1804      v1.0.0             5f6780a10683   3 years ago   931MB
    ```

3. 이미지 실행
    ```shell
    sudo docker run -p "80:80" --name lamp -d -v ${PWD}/app:/app -v ${PWD}/mysql:/var/lib/mysql my-lamp-1804
    ```

4. 아까보다 뭔가 할일은 많아지고 파일도 하나 생기고 더 복잡해지기만 했지 장점이 안보입니다. 하지만 이걸 활용하면 아래와 같은걸 할 수 있습니다. 컨테이너 내부에서 명령어를 실행하고 파일을 카피하거나 라이브러리를 다운로드하고 환경변수를 설정할 수 있습니다.

    이걸 Dockerfile 없이 위와 같은 명령문으로 이 작업을 하려면 컨테이너를 띄우고 직접 컨테이너 안으로 들어가서 이 작업을 해줘야합니다. 그래서 당장은 필요 없을지 몰라도 결국엔 쓰게 됩니다.


    ```dockerfile
    # 베이스 이미지로 LAMP 스택 사용
    FROM mattrayner/lamp:latest-1804

    # 제작자
    MAINTAINER AuspiciousBlessing <AuspiciousBlessing83@gmail.com>

    # 이 파일의 설명
    LABEL Description="This is an example" \
          License="Apache License 2.0" \
          Usage="sudo docker run -p "80:80" --name lamp -d -v ${PWD}/app:/app -v ${PWD}/mysql:/var/lib/mysql my-lamp-1804" \
          Version="1.0.0"

    # 볼륨 지정
    VOLUME ["/app", "/var/lib/mysql"]

    # 명령어 실행
    RUN apt-get update
    RUN apt-get upgrade -y

    # 파일 카피
    COPY debconf.selections /tmp/

    # 라이브러리 다운로드
    RUN apt-get install -y zip unzip
    RUN apt-get install git nodejs npm composer nano tree vim curl ftp -y
    RUN npm install -g bower grunt-cli gulp

    # 환경변수 설정
    ENV LOG_STDOUT **Boolean**
    ENV LOG_STDERR **Boolean**
    ENV LOG_LEVEL warn
    ENV ALLOW_OVERRIDE All
    ENV DATE_TIMEZONE UTC
    ENV TERM dumb

    # Apache 실행
    CMD ["/run.sh"]
    ```

<br>
## The second evolution, Docker-compose
Docker Compose는 2014년 12월에 첫 번째 버전으로 출시되었습니다. 원래는 Fig라는 이름으로 시작했으며, Docker Inc.에 의해 2014년에 인수된 후, Docker Compose로 이름이 바뀌었습니다.

다중 컨테이너 애플리케이션을 정의하고 관리하기 위한 도구입니다. 이를 통해 여러 개의 Docker 컨테이너를 함께 정의하고 실행할 수 있습니다. Docker Compose는 YAML 파일을 사용하여 애플리케이션의 서비스, 네트워크, 볼륨 등을 선언적으로 구성할 수 있습니다. 기본적으로 Compose는 각 서비스마다 별도의 컨테이너를 정의하고, 이들이 서로 연결될 수 있도록 설정합니다.

### Using Docker-compose
이 방법을 사용해도 위와 동일한 결과를 보여줍니다.

1. docker-compose.yml라는 파일명으로 docker-compose 파일 생성

    ```yaml
    version: '3'
    services:
      lamp:
        image: mattrayner/lamp:latest-1804
        container_name: lamp
        ports:
          - "80:80"
        volumes:
          - ./app:/app
          - ./mysql:/var/lib/mysql
        restart: always
    ```
  설명:  
  - version: Compose 파일의 버전 (version: '3'은 Docker Compose에서 권장되는 최신 버전 중 하나입니다).
  - services: 여러 컨테이너를 정의하는 섹션입니다. 여기서는 lamp 서비스 하나만 있습니다.
  - image: 사용할 Docker 이미지 (mattrayner/lamp:latest-1804).
  - container_name: 컨테이너의 이름을 lamp로 지정.
  - ports: 호스트의 포트 80을 컨테이너의 포트 80에 매핑.
  - volumes: 호스트 디렉터리(./app, ./mysql)를 컨테이너의 디렉터리(/app, /var/lib/mysql)에 마운트.
  - restart: 컨테이너가 종료될 때 자동으로 다시 시작하도록 설정 (always는 항상 재시작하도록 지정).

2. 실행
   Docker-compose를 사용하면 정말 진보되었다는 것을 알 수 있습니다. 유의할 점은 컨테이너를 만들 때 Docker만 사용하는 것과는 명령어가 달라졌다는 것입니다.
   ```shell
   sudo docker-compose up -d  # 데몬으로 실행
   sudo docker-compose down   # 중지
   ```
  
3. Dockerfile을 쓸 때 docker run 하던 부분의 명령줄이 전부 docker-compose.yml에 들어왔는데 Dockerfile은 여전히 이미지 내부의 세팅에 쓰입니다. 위의 4번에서 만든 복잡한 Dockerfile을 쓴다고 가정해봅시다. 그럼 docker-compose 파일은 이렇게 한줄만 바꿔주면 됩니다.
    ```yaml
    version: '3'
    services:
      lamp:
        image: . # 경로를 나타내며 현재 경로에 Dockerfile이 존재시
        container_name: lamp
        ports:
          - "80:80"
        volumes:
          - ./app:/app
          - ./mysql:/var/lib/mysql
        restart: always
    ```

## In conclusion
이정도면 Docker와 Docker-compose에 대한 모든 실습을 마친 것 같습니다. 더 필요한 부분이 생각이 나거나 요청이 들어오면 업데이트 될 수 있습니다.
