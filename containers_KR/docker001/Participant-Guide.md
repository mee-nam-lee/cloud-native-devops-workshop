# 컨테이너 실험 실습실


이 Hands on Lab (Hands on Lab)은 참가자들에게 컨테이너 화의 기초를 배우고 그 장점을 탐색하며 초보 수준의 실습으로 Docker 기술을 소개합니다. 이 2 시간 세션에서 다룰 주제는 다음과 같습니다. 

1. [Intro to Basic Container Concepts](Participant-Guide.md#intro-to-basic-container-concepts) 
2. [Verify Docker Engine Hands on Lab Environment](Participant-Guide.md#verify-docker-engine-hands-on-lab-environment) 
3. [Hello Helloworld](Participant-Guide.md#hello-helloworld) 
5. [Create a Dockerfile and Docker Image](Participant-Guide.md#create-a-dockerfile-and-docker-image) 
6. [Push an Image to your Docker Hub Account](Participant-Guide.md#push-an-image-to-your-docker-hub-account) 
7. [Install Docker Compose](Participant-Guide.md#install-docker-compose) 
8. [Create Wordpress "stack"](Participant-Guide.md#create-a-wordpress-stack) 
9. [Basics of Persistent storage](Participant-Guide.md#basics-of-persistent-storage) 
10. [Use Github and Docker Hub together to build an Image and Run the Container](Participant-Guide.md#use-github-and-docker-hub-together-to-build-an-image-and-run-the-container) 
11. [Demo of Oracle Container Cloud Service Showing Participant's Containers](Participant-Guide.md#demo-of-oracle-container-cloud-service-showing-participants-containers) 



### 이 HOL을 완료하기위한 요구 사항 :


*사전 구성된 Docker-Engine 환경 - [Intro to Basic Container Concepts](Participant-Guide.md#intro-to-basic-container-concepts) 참조 

*인터넷 접속 

*노트북 

*메모 및 스 니펫을 계속 유지하는 텍스트 편집기 

*Docker 허브 계정 

*Github 계정 

***

## 기본 컨테이너 개념 소개


컨테이너는 Docker 이미지의 런타임 인스턴스입니다. 

[Intro to Basic Container Concepts](Participant-Guide.md#intro-to-basic-container-concepts) 

Docker는 회사 및 컨테이너 화 기술입니다. 

[Verify Docker Engine Hands on Lab Environment](Participant-Guide.md#verify-docker-engine-hands-on-lab-environment) 

컨테이너는 오랫동안 사용되어 왔습니다. Docker는 사람들로 하여금 단순한 사용할 수 있는 기술을 개발했으며 이전보다 훨씬 이해하기 쉬웠습니다. 따라서 **휴대용 및 경량** 응용 프로그램 패키징 기술을 개발하는 데 엄청난 지원을 얻었습니다.

그리고 컨테이너 기술의 변화는 아직도 계속되고 있습니다. 몇 년 동안 우리가 겪어왔던 몇 가지 기술에 대해 알아보겠습니다. 

리눅스 컨테이너의 역사 : 

<img src=images/002-container-history.png />



이제 가상 머신 (VM)이 컨테이너와 어떻게 다른지 살펴 보겠습니다. 

컨테이너는 VM처럼 들릴 수 있지만 두 기술은 서로 다른 기술입니다. VM을 사용하면 각 가상 컴퓨터에 응용 프로그램, 필요한 바이너리 및 라이브러리, **전체 게스트 운영 체제가 포함됩니다.**

반면에 컨테이너는 응용 프로그램과 모든 종속성을 포함하지만 커널을 다른 컨테이너와 공유하며 호스트에 Docker 엔진을 설치하는 것 이외의 특정 인프라에 묶이지 않습니다. 거의 모든 컴퓨터, 인프라 및 응용 프로그램에서 컨테이너를 실행할 수 있습니다. 

<img src=images/002-vm-vs-container.png />



>*참고 - 현재 Windows 및 Linux 컨테이너는 해당 커널 기반에서 실행해야하므로 Windows 컨테이너는 Linux 호스트에서 실행될 수 없으며 그 반대의 경우도 가능합니다.*

Docker 이미지는 컨테이너 내부에서 소프트웨어 응용 프로그램을 실행하는 데 필요한 모든 것을 가진 파일 모음입니다. 그러나 컨테이너가 실행되는 동안 컨테이너 내부에 작성된 모든 데이터는 유지되지 않습니다. 

컨테이너가 이미지에서 중지되었다가 다시 시작되면 컨테이너는 마지막 실행주기 동안 변경된 내용이 없는 처음과 완전히 동일하게 실행됩니다. 컨테이너의 변경 사항은 이미지 작성 프로세스 중에 이미지의 일부가되는 Dockerfile을 사용하여 작성하거나 컨테이너 내부에서 외부로 영구 저장 장치 볼륨을 마운트하여 데이터를 유지할 수 있습니다. 이것은 아래의 HOL 연습에서 더 자세히 살펴볼 것입니다. 

<img src=images/004-docker-images.jpg />



약간 뒤로 돌아 가면 Docker가 소개하는 새로운 명명법이 있습니다. 여기에 익숙해 져야 할 용어가 있습니다. 

이 Docker 기술 각각은 HOL에서 탐구 될 것입니다. 이 핵심 기술은 오픈 소스입니다. 더 큰 생태계에는 유료 지원 옵션이있는 오픈 소스 또는 라이센스 또는 하이브리드 일 수 있는 다른 기술이 있습니다. 

<img src=images/005-docker-terms.jpg />



Docker 엔진은 컨테이너를 실행할 수있는 핵심 기술입니다. 컨테이너가 모든 Linux 호스트에서 실행 되려면 최소한 Docker Engine이 설치되어 있어야합니다. 그런 다음 Docker Engine이 설치된 모든 Linux 호스트에서 컨테이너를 실행할 수 있으므로 각 호스트에서 응용 프로그램 별 구성 변경 없이도 이식성의 이점을 얻을 수 있습니다. 

<img src=images/004-docker-engine.jpg />



좋습니다, 그것들은 기술의 메카니즘 중 일부입니다 만, Docker가 모든 유형의 IT 사람들에게 인기가있는 이유는 무엇입니까? Developers 및 IT Ops의 관점을 살펴 보겠습니다. 

<img src=images/004-why-containers.jpg />



또한 Docker를 탐색하고 사용하는 수백 개의 조직과 이야기 할 때 Docker가 제공하는 핵심 이점이 있습니다. 

<img src=images/005-docker-usage.jpg />



이 모든 것은 여러 가지 측면에서 기술 혁신의 일부이며 Modern하고 민첩한 애플리케이션 개발의 기반이 됩니다. 

<img src=images/006-evolution.jpg />


***

## Docker 엔진이 랩 환경에서 작동하는지 확인


이 첫 번째 섹션에서는 [Prerequisites document](Prerequisites.md)에서 요청한대로 Docker Engine 환경에 연결할 수 있는지 확인합니다. 지금 환경에 액세스하여 터미널에서 다음 명령을 실행하십시오. 

> 참고 - Oracle Container Cloud Service 인스턴스에서 Docker Engine 환경으로 Worker Node 중 하나를 사용하는 경우 [access it via SSH per these instructions](supplemental/Access-OCCS-VM-SSH.md) 

**선택 사항**- 편의상 root로 실행되므로 sudo로 모든 것을 시작하지 않아도됩니다 (Windows 용 Docker를 실행하는 경우에는 적용되지 않음). 

```
$ sudo -s
```


다음은 설치된 버전을 확인하는 Docker 전용 명령입니다. 

```
$ docker --version
```


Docker가 설치되어 실행 중이면 다음과 같은 출력이 표시됩니다. 

```
Docker version 1.1x.x, build 57bf6fd
```


***

## 안녕하세요 헬로우 월드


Docker의 Hello World 예제를 실행합니다. 

	
```
$ docker run hello-world
```


&quot;hello-world&quot;이미지는 호스트에서 로컬로 사용할 수 없으므로 명령은 공용 Docker 허브 이미지 저장소에서 hello-world 이미지를 자동으로 가져 와서 포 그라운드에서 컨테이너를 실행합니다. 

<img src=images/2017-03-16_13-40-42.jpg />


***

**축하합니다. 첫 번째 Docker 컨테이너를 실행했습니다!**

모든 컨테이너를 나열하십시오 : 

>*참고 - "- a" option = running **and** stopped*

```
$ docker ps -a
```
hello-world 컨테이너가 한 번 실행 된 다음 종료되었습니다. 

<img src=images/2017-03-16_14-46-49.jpg />


***

이 연습에서는 Docker Hub에서 다른 Docker 이미지를 탐색합니다. 

**Docker Hub에서 공개 이미지 Helloworld 예제를 찾아보십시오. 그것을 실행하십시오.**

이 Docker 허브 이미지 사용 : 

[https://hub.docker.com/r/karthequian/helloworld](https://hub.docker.com/r/karthequian/helloworld) 

Docker 허브 레지스트리에서 이미지를 가져옵니다. 

>*참고 - 레이어가 개별적으로 어떻게 당겨 지는지 관찰하십시오. 도커 이미지 파일은 여러 레이어로 구성되어 있으며 자세한 내용은 [Docker docs here about images and layers](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/)*

```
$ docker pull karthequian/helloworld:latest
```


Docker Hub 페이지에서 Docker Run 명령을 복사 / 붙여 넣기하고 &quot;-d&quot;옵션을 추가하여 컨테이너가 &quot;detached&quot;모드로 실행되도록하십시오 : 

>*참고 - &quot;-d&quot;옵션은 마지막 연습에서 보았던 전경 모드와 달리 분리 모드로 컨테이너를 실행합니다. 이것의 이점은 더 이상 실행중인 컨테이너의 경우 터미널 창을 비울 수 있다는 것입니다.*

```
$ docker run -d -p 80:80/tcp "karthequian/helloworld:latest"
```


브라우저에서 Helloworld 앱을 탐색하십시오. 실행중인 Docker Host의 IP로 이동하여 방문수를 기록하십시오. 

>*참고 - IP는 http : // host_ip 또는 로컬 호스트의 http : // localhost에 SSH 할 호스트와 동일합니다 (이 문서의 나머지 부분에서는 단순화를 위해 호스트 IP 또는 도커 호스트 IP)*


<img src=images/004-hello-world.png />


***

이제 Docker 컨테이너에있는 응용 프로그램을 실제로 사용하고 있습니다. 브라우저를 새로 고침하고 방문수가 어떻게 증가하는지 관찰합니다. 이것은 실제 응용 프로그램입니다. 간단한 예제이지만 컨테이너에서 실행중인 응용 프로그램 사용 경험의 예입니다. 컨테이너에서 실행되지 않는 경우와 다를 바 없습니다. 

>*매일 매일 얼마나 많은 앱을 사용하고 있는지, 실제로 Docker 컨테이너에서 실행 중인지 궁금합니다.*

이제 Docker가 실행중인 Helloworld 컨테이너를 할당 한 이름을 살펴보십시오. 

실행중인 모든 컨테이너 나열 : 

```
$ docker ps
```


Docker가 아래에 &quot;ecstatic_lamport&quot;와 같은 컨테이너 이름을 지정했는지 확인하십시오. 도커가 컨테이너에 어떤 이름을 지었습니까? 우리가 조금 그것을 사용할 것이기 때문에,이 이름을 기억하십시오. 

<img src=images/2017-03-16_13-49-25.jpg />


***

>*참고 - 컨테이너 이름을 지정하지 않으면 Docker는 비슷한 두 부분 이름을 자동으로 할당합니다*

**더 구체적인 이름의 컨테이너를 중지하고 다시 실행하십시오**

이제 터미널 창으로 돌아가서 컨테이너를 멈추고 더 많은 설명이 포함 된 이름을 지정하면 실행중인 컨테이너가 많은 경우 쉽게 찾을 수 있습니다. 

실행중인 컨테이너 중지 - 아래 **your_container**를 실행중인 컨테이너의 실제 이름으로 바꿉니다. 

```
$ docker stop your_container
```


이제 &quot;rm&quot;명령을 사용하여 컨테이너를 제거하십시오. 

```
$ docker rm your_container
```


컨테이너가 제거되었는지 확인하십시오. 

```
$ docker ps -a
```


> 주 - 컨테이너는 이름**(종속 이미지 레이어가없는 경우)**, 긴 ID 또는 짧은 ID*를 사용하여 중지하고 제거 할 수 있습니다. 

이제 &quot;helloworld_app&quot;와 같이 더 알기 쉬운 이름으로 컨테이너를 실행하십시오. 

```
$ docker run -d --name helloworld_app -p 80:80/tcp "karthequian/helloworld:latest"
```


실행중인 모든 컨테이너를 다시 나열하십시오. 

```
$ docker ps
```


>*컨테이너를 쉽게 찾을 수 있습니까? 특히 컨테이너 이름의 컨텍스트가 있습니까? 특히 많은 컨테이너가 실행중인 경우*

컨테이너를 중지하고 제거하십시오. 

```
$ docker stop helloworld_app

$ docker rm helloworld_app
```


우리는 HOL의이 부분을 완성합니다. 

***

## Dockerfile 및 Docker 이미지 만들기


이 연습에서는 Dockerfile에서 자신의 이미지를 빌드합니다. 

**DockerFiles 정보**

Dockerfile은 기본 이미지 (일반적으로 Alpine Linux와 같은 얇은 Linux OS 배포판)로 시작한 다음 응용 프로그램 및 구성에 레이어를 지정하는 방법입니다. [According to Docker](https://docs.docker.com/engine/reference/builder/) : 

*&quot;Dockerfile은 이미지를 어셈블하기 위해 사용자가 명령 줄에서 호출 할 수있는 모든 명령을 포함하는 텍스트 문서입니다 .Docker 빌드 사용자는 여러 명령 줄 명령을 연속적으로 실행하는 자동화 된 빌드를 만들 수 있습니다.&quot;*

**도커 이미지 만들기**

[Docker Whalesay](https://hub.docker.com/r/docker/whalesay/) 예제를 사용하여 첫 번째 이미지를 만듭니다. 

다음 단계를 따르십시오. 

홈 디렉토리에서 Dockerfile을 저장할 디렉토리를 만듭니다. 

```
$ cd ~ 

$ mkdir mydockerbuild
```


새 디렉토리로 변경하십시오. 

```
$ cd mydockerbuild
```


1. 3 단계에서 VI 또는 nano와 같이 선택한 편집기를 사용하십시오. 

Oracle Linux를 사용하는 경우 VI를 사용하십시오. 

>*주 - 대문자는 파일 이름 &quot;Dockerfile&quot;에서 중요합니다. 나머지 문자는 대문자 D와 소문자를 사용하십시오.*

```
$ vi Dockerfile
```


다음 세 줄의 Dockerfile이라는 텍스트 파일을 만듭니다. 

>*참고 - VI를 사용하는 경우 붙여 넣기 전에 삽입 모드로 들어가기 위해 먼저 &quot;i&quot;키를 누르십시오. 

```
FROM docker/whalesay:latest

RUN apt-get -y update && apt-get install -y fortunes

CMD /usr/games/fortune -a | cowsay
```


1. 8 단계에서 VI가있는 Dockerfile에 3 줄을 추가 한 후에 Esc 키 - 콜론 -w (쓰기) - q (종료)를 입력하여 파일을 저장하십시오. 

	
```
esc : w q 
```


Dockerfile의 내용이 올바른지 확인하십시오. 

```
$ cat Dockerfile
```


>*참고 - VI 용 문서는 다음과 같습니다 : [https://www.cs.colostate.edu/helpdocs/vi.html](https://www.cs.colostate.edu/helpdocs/vi.html)*

그런 다음 섹션 2에서 Docker 이미지를 작성하고 &quot;.&quot; 명령의 끝에서 : 

```
$ docker build -t docker-whale .
```


그런 다음 섹션 4에서 호스트의 이미지를 나열하고 도커 - 고래 이미지를 컨테이너로 실행하십시오. 

```
$ docker images
```


```
$ docker run docker-whale
```


터미널에서 출력을 확인하면 컨테이너가 한 번 실행 된 다음 중지됩니다. 

<img src=images/2017-03-16_14-10-47.jpg /> 


***

## 이미지를 도커 허브 계정에 푸시


**레지스트리**

레지스트리는 Docker 이미지를 저장합니다. Docker를 랩톱에서 떼어내는 첫 번째 단계는 레지스트리를 사용하는 것입니다. 가장 널리 사용되는 레지스트리는 Docker Hub : [https://hub.docker.com](https://hub.docker.com)입니다. 

>*참고 -이 연습에서는 공용 Docker 레지스트리를 사용하려면 Docker Hub 계정이 필요합니다. 이미 가지고 있지 않다면 무료로 가입 할 수 있습니다 : [https://hub.docker.com/](https://hub.docker.com/)*

**태그를 달고 새로운 이미지를 Docker Hub 레지스트리에 푸시하십시오. 이 연습에서는 사용자 이름이 Docker 허브 계정 이름이됩니다.**

먼저 터미널에서 Docker 허브 계정에 로그인하십시오. 

```
$ docker login
```


메시지가 나타나면 Docker 계정 사용자 이름 (소문자), 비밀번호 및 이메일을 입력하십시오. 

이제 Docker Hub에서 새 docker-whale 이미지에 태그를 달고 계정에 푸시하십시오. 

Docker**사용자 이름**을 다음으로 대체하십시오. 

```
$ docker tag docker-whale:latest username/docker-whale:latest
```


Docker 이미지를 계정으로 푸시합니다. 그러면이 이미지에 대해 &quot;docker-whale&quot;이라는 새 저장소가 만들어집니다. 

```
$ docker push username/docker-whale:latest
```


Docker 허브에서 귀하의 계정 페이지로 이동하여**사용자 이름**을 대체하십시오. 

[https://hub/docker.com/r/username](https://hub.docker.com/r/username) 

당신이 밀어 넣은 이미지가 보이나요? 

<img src=images/010-docker-hub.png />


***

이제 로컬 이미지를 제거하고 Docker Hub 레지스트리에서 이미지를 가져 와서 실행하십시오. 

이렇게하려면 중지 된 컨테이너를 이름이 아닌 짧은 ID를 사용하여 먼저 제거해야합니다. 짧은 아이디 찾기 : 

```
$ docker ps -a 
```


해당 컨테이너의 짧은 ID를 복사하면 ee31fe1dd8f8 형식과 유사하게되며 &quot;rm&quot;명령을 사용하여 컨테이너를 제거하십시오. 

```
$ docker rm short_id
```


컨테이너가 제거되었으므로 이미지를 호스트에서 로컬로 제거하고 Docker 허브의 이미지에서 컨테이너를 강제로 실행할 수 있습니다. &quot;rmi&quot;명령을 사용하여 이미지를 제거하십시오. 

Docker 허브에 푸시 한 이미지를 로컬에서 제거하십시오. 

```
$ docker rmi username/docker-whale
```


이미지가 호스트에서 제거되었는지 확인하십시오. images 명령을 사용하여 모든 Docker 이미지를 봅니다. 

```
$ docker images
```


이제 Docker Hub의 리포지토리에서 이미지를 직접 실행하고 이미지가 로컬에 존재하지 않기 때문에 이미지를 새로 가져와야합니다. 

```
$ docker run username/docker-whale
```


> 참고 - 태그가 사용되지 않으면 기본 태그는 &quot;latest&quot;이며 레지스트리에서 가져옵니다*

<img src=images/2017-03-16_14-17-38-2.jpg />


***

**이 시점에서 모든 컨테이너를 중지하고 제거하십시오. 모든 컨테이너에서이 작업을 수행하려면 다음 명령을 사용하십시오.**

```
$ docker stop $(docker ps -a -q)

$ docker rm $(docker ps -a -q)
```


***

## Docker 설치 Compose



**Docker 소개 Compose**

Docker Compose 란 무엇입니까? 왜 사용합니까? 

Docker에 따르면*Docker Compose는 다중 컨테이너 Docker 응용 프로그램을 정의하고 실행하기위한 도구입니다. 작성을 사용하면 작성 파일을 사용하여 응용 프로그램의 서비스를 구성 할 수 있습니다. 그런 다음 단일 명령을 사용하여 구성에서 모든 서비스를 만들고 시작하십시오.*

**Docker Compose 설치**

>*이 HOL에서 사용될 수있는 다양한 Linux 환경에서 경로 문제가 발생하지 않도록 루트 홈 디렉토리 아래에 &quot;compose&quot;라는 디렉토리에 Docker Compose v1.12를 설치합니다. 또한 Docker Compose를 해당 디렉토리에서 로컬로 실행하고 첫 번째 docker-compose.yml 파일을 만듭니다. 

루트 홈 디렉토리로 변경하십시오. 

```
$ cd ~
```


루트 홈 디렉토리에 있는지 확인하십시오. 

```
$ pwd
```


&quot;compose&quot;라는 새 디렉토리를 만듭니다. 

```
$ mkdir compose
```


이 새 디렉토리로 변경하십시오. 

```
$ cd compose
```


그런 다음이 curl 명령을 사용하여 해당 디렉토리에 Docker Compose v1.12를 로컬로 설치하십시오. 

```
$ curl -L "https://github.com/docker/compose/releases/download/1.12.0/docker-compose-$(uname -s)-$(uname -m)" -o docker-compose
```


실행 권한을 변경하십시오. 

```
$ chmod +x docker-compose
```


설치된 Docker Compose 버전을 확인하고 확인하십시오. 

```
$ ./docker-compose --version
```


>*참고 - 자세한 내용은 나중에 Docker 문서를 참조하십시오 : [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)*
***

## Wordpress &quot;스택&quot;만들기


간단한 Wordpress 스택을 만들려면 다음 단계를 따르십시오. 

편집기 또는 VI를 사용하여 &quot;docker-compose.yml&quot;파일을 생성하십시오 : 

>*참고 - 위의 Dockerfile과 마찬가지로 파일 이름의 대소 문자가 중요합니다. &quot;docker-compose.yml&quot;에 대해 모두 소문자 사용*

```
$ vi docker-compose.yml
```


다음 텍스트 또는 YAML을 복사하여 붙여 넣으십시오. 

```
version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: wordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "80:80"
     restart: always
     volumes:
       - /var/www/html:/var/www/html:rw
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
     db_data:
```



docker-compose.yml을 저장하십시오. 

VI를 사용한다면 Esc 키를 콜론 -w (쓰기) - q (종료)라고 입력하여 파일을 저장하십시오 : 

	
```
esc : w q 
```


docker-compose.yml 파일의 내용이 올바른지 확인하십시오. 

```
$ cat docker-compose.yml
```


이 명령으로 Wordpress 스택을 실행하십시오 : 

```
$ ./docker-compose up -d
```


**Wordpress 설정 페이지를 방문하여 실행중인 스택을 확인하십시오.**

브라우저에서 호스트 IP를 사용하여 아래 URL을 복사하여 Wordpress 설정을 시작하십시오. 

```
http://host_ip/wp-admin/install.php
```


>*주 - Mac 사용자 용 Docker - 다음 오류가 발생하는 경우 Mac에서 Docker 서비스를 다시 시작하여 / var / www / html*

```
ERROR: for wordpress  Cannot start service wordpress: Mounts denied: 
The path /var/www/html
is not shared from OS X and is not known to Docker.
You can configure shared paths from Docker -> Preferences... -> File Sharing.
See https://docs.docker.com/docker-for-mac/osxfs/#namespaces for more info.
```


**축하합니다. Docker에서 첫 번째 Wordpress 앱을 성공적으로 시작했습니다!**

이 스택에 대한 자세한 내용은 [https://docs.docker.com/compose/wordpress/](https://docs.docker.com/compose/wordpress/)를 참조하십시오. 

***

## 영구 저장소의 기본 사항


**Docker 볼륨 이해**

이 섹션에서는 호스트 데이터 볼륨을 사용하여 데이터 지속성을 살펴 봅니다. 

Docker 볼륨에 대한 전체 소개는 다음 위치에 있습니다. [https://docs.docker.com/compose/wordpress/](https://docs.docker.com/compose/wordpress/) 

즉, 컨테이너 볼륨이 영구 호스트 볼륨에 마운트되어 있지 않으면 컨테이너가 제거 될 때 컨테이너 내에 저장된 모든 데이터가 손실됩니다. 

이제 방금 사용했던 Wordpress 스택에서 데이터가 지속되는 방식을 살펴 보겠습니다. 

가장 중요한 것은, Docker Compose YAML 파일에서 Wordpress와 DB를위한 두 개의 볼륨 문을 사용했습니다. 

예를 들어, YAML for Wordpress에있는이 문은 이미지를 블로그 게시물에 보관할 수있게 해줍니다. 이 예에서는 호스트 볼륨에 데이터가 저장되는 위치를 명시하고 있습니다. 
```
     volumes:
       - /var/www/html:/var/www/html:rw
```


데이터베이스에 대한이 볼륨 문. 이 예에서 &quot;db_data&quot;가 호스트 볼륨에 저장되는 위치를 Docker가 매핑하도록 허용합니다. 

```
     volumes:
       - db_data:/var/lib/mysql
 ```
호스트 볼륨이 먼저 나열된 다음 컨테이너 볼륨이 콜론으로 구분됩니다. 지정된 컨테이너 볼륨 경로에 기록 된 모든 데이터를 호스트 볼륨에 바인드합니다. 컨테이너가 중지되고 동일한 호스트에서 다시 실행되면 호스트 볼륨에서 기존 데이터를 가져옵니다. 

*이제 우리가 탐구 할 마법을 알게되었습니다.*

**Wordpress 설정을 완료하고 블로그 게시물을 만드십시오.**

브라우저에서 Host_IP로 이동하여 다음과 같이 Wordpress 초기화 URL : /wp-admin/install.php와 함께 추가하십시오. 

>*참고 - 위의 Docker Compose로 배포 할 때 보았던 것과 동일한 설정 URL입니다. 이미 브라우저 탭에로드되어있을 수 있습니다.*


```
http://docker_host_ip/wp-admin/install.php
```


먼저 언어를 선택하십시오. 

<img src=images/033-wp-setup1.png />


***

Wordpress 로그인 정보를 설정하십시오. 노트에 사용자 이름과 비밀번호를 보관하십시오. 

<img src=images/034-wp-setup2.png />


***

Wordpress에 로그인하려면 &quot;로그인&quot;버튼을 클릭하십시오 : 

<img src=images/034-wp-setup2.png />


***

이전에 생성 한 자격 증명을 사용하여 로그인하십시오. 

<img src=images/036-wp-login2.png />


***

다음 단계 섹션에서 &quot;첫 번째 블로그 게시물 작성&quot;을 선택하십시오. 

<img src=images/037-write-blog.png />


***

샘플 블로그 게시물을 만드십시오. 원하는 경우 이미지를 포함하고 게시를 클릭하십시오. 

<img src=images/038-publish-blog.png />


***

블로그 게시물로 이동하려면 &quot;Permalink&quot;를 클릭하십시오 : 

<img src=images/039-permalink.png />


***

블로그 게시물의 퍼머 링크 URL을 복사하여 나중에 메모에 남겨 두십시오. 나중에 필요할 수 있습니다. 

<img src=images/040-view-blog.png />


***

실행중인 Wordpress 및 Database 컨테이너를 짧은 ID로 중지하고 제거하십시오. 

이전 실습에서 이것을 기억하십시오 : 

```
$ docker ps -a

$ docker stop short_id

$ docker rm short_id
```


모든 컨테이너가 중지되고 제거 될 때까지 다음 컨테이너에 대해 반복하거나 이전에 표시된 대량 제거를 사용하십시오. 


페이지를 새로 고침하여 Wordpress 블로그 게시물이 사라 졌는지 브라우저에서 확인하십시오. 

<img src=images/043-refresh.png />


***

Wordpress 스택 재배포 : 

```
$ ./docker-compose up -d
```


브라우저에서 기록한 블로그 게시물 URL로 다시 이동하여 페이지를 새로 고칩니다. 

<img src=images/047-refresh-blog.png />


***

데이터는 호스트 볼륨에 쓰여지고 동일한 호스트에 재배포 될 때 컨테이너에 다시 연결되기 때문에 지속됩니다. 


**다음 섹션으로 이동하기 전에 모든 컨테이너를 중지하고 제거하십시오 :** 

```
$ docker stop $(docker ps -a -q)

$ docker rm $(docker ps -a -q)
```


***


## GitHub와 Docker Hub를 함께 사용하여 이미지를 만들고 컨테이너를 실행하십시오.


**요구 사항 : GitHub 및 Docker 허브의 사용자 계정**

>*참고 - Github 계정이 없으면 여기에서 무료 계정을 만드십시오 : [https://github.com/join](https://github.com/join)*

이제 GitHub 및 Docker Hub를 사용하여 이미지를 만드는 또 다른 방법을 살펴 보겠습니다. 

>*참고 -이 연습에서는 hello-earth라는 저장소와 같은 기존의 hello-world를 포크 한 다음 웹 페이지를 수정합니다. GitHub의 Index.html은 Docker 허브에서 자동화 된 Docker 이미지 빌드를 트리거합니다. 그런 다음 성공적인 빌드를 확인하고 Docker 환경에서 이미지를 컨테이너로 실행합니다.*


**시작하려면이 GitHub Docker001 레포를 자신의 포크로 포크하십시오**

로그인 GitHub 계정 : 

https://github.com/login 

브라우저에서 다음 GitHub 저장소로 이동합니다. 

https://github.com/oracle/cloud-native-devops-workshop/tree/master/containers/docker001 


특정 GitHub 저장소에 대해 &quot;포크&quot;버튼을 선택하십시오 : 

<img src=images/github-dockerhub_14.jpg />


***

이렇게하면이 저장소가 자신의 GitHub 계정에 자동으로 복사되며 필요한 경우 GitHub 계정을 편집 할 수 있습니다. 

<img src=images/github-dockerhub_9.jpg />


***

이제 브라우저의 다른 탭에서 Docker 허브 계정에 로그인하십시오. 

https://hub.docker.com/login 


Docker Hub 계정 내에서 Create 아래의 Top Menu에서 &quot;Create Automated Build&quot;를 선택하십시오. 

<img src=images/github-dockerhub_13.jpg />


***

Docker 허브가 소스 코드를 가져올 수 있도록 GitHub 계정을 연결하라는 메시지가 표시됩니다. 

<img src=images/2017-03-16_10-41-09.jpg />


***

다음과 같이 GitHub를 선택하십시오. 

<img src=images/2017-03-16_10-41-14.jpg />


***

공개 및 비공개 리포지토리 모두 선택 : 

<img src=images/2017-03-16_10-41-23.jpg />


***

다시 말하지만 Docker Hub 계정에서 Create 아래의 Top Menu에서 &quot;Create Automated Build&quot;를 선택하십시오. 

<img src=images/github-dockerhub_13.jpg />


***

Create Auto-Build :를 선택하십시오. 

<img src=images/github-dockerhub_11-2.jpg />


***

&quot;cloud-native-devops-workshop&quot;저장소를 선택하십시오 : 

<img src=images/github-dockerhub-21.jpg />


***

저장소 이름을 &quot;hello-earth&quot;로 만들고 간단한 설명을 추가하고 저장을 누릅니다. 

> 주 - 저장소 이름을 지정하면 첫 번째 빌드를 수행 한 후에 이미지 이름이 &quot;hello-earth&quot;가됩니다.*

<img src=images/github-dockerhub_10.jpg />


***

Build Settings 탭에서 Dockerfile Location에 대해 &quot;/ containers / docker001 / lab1&quot;을 입력하고 &quot;Save Changes&quot;버튼을 누릅니다. 

<img src=images/github-dockerhub-20.jpg />


***

GitHub 계정으로 돌아가서 위의 Docker001 저장소를 분기 한 URL로 이동하여 &quot;lab1&quot;폴더를 엽니 다. 아래 URL에 GitHub 사용자 이름을 바꿉니다. 

https://github.com/*username*/cloud-native-devops-workshop/tree/master/containers/docker001/lab1 

GitHub 페이지에서 &quot;Index.html&quot;링크를 클릭하십시오 : 

<img src=images/2017-03-16_11-15-12.png />


***

이 Index.html을 수정하여 새 &quot;Hello Earth&quot;웹 페이지를 만들면 Docker 허브에 새로운 이미지 빌드가 자동으로 트리거됩니다. 그런 다음 결과 이미지를 컨테이너로 실행하여 변경 사항을 관찰합니다. 

연필 아이콘을 통해 페이지를 수정하십시오. 

<img src=images/050-edit-index.png />


***

Line 12를 다음과 같이 변경하여 myName 및 myCity가 표시된 사용자 이름과 도시를 대체하십시오. 

<img src=images/2017-03-16_11-19-42.jpg />


***

아래로 스크롤하여 변경 사항 적용. 설명을 추가하고 &quot;Commit Changes (변경 사항 적용)&quot;버튼을 누릅니다. 

<img src=images/052-commit-index.png />


***

그러면 DockerHub에서 DockerHub의 새로운 자동 빌드가 실행되고, Dockerfile은 빌드 프로세스의 일부로 Index.html의 새로운 변경 사항을 통합합니다. 상태는 &#39;Build Details (빌드 세부 정보)&#39;탭에 표시됩니다. 빌드 상태에 대한 업데이트를 보려면 브라우저를 새로 고침해야합니다. 

>*참고 - 자동 빌드가 자동으로 실행되지 않는 경우 Docker 허브의 &quot;트리거&quot;버튼을 사용하여 빌드 설정 탭을 수동으로 시작하여 이미지 빌드를 시작할 수 있습니다.*

<img src=images/github-dockerhub_3.jpg />


***

Docker Hub에서 빌드를 완료하는 데 몇 분이 소요됩니다. 성공하면 Status 열에 Success가 표시됩니다. 

>*참고 - 업데이트 된 상태를 보려면 브라우저 탭을 새로 고침해야 할 수도 있습니다.*

<img src=images/github-dockerhub_1.jpg />


***

빌드가 성공적이면 Docker CLI 환경으로 돌아가서 새 컨테이너를 실행하십시오. 아래 명령에서 &quot;username&quot;에 대한 Docker Hub 이름을 바꿉니다. 

```
$ docker run -d -p 80:80 "username/hello-earth"
```


컨테이너가 실행되면 도커 호스트의 IP를 방문하여 방금 빌드하고 실행 한 새로운 hello-earth 컨테이너에 대한 변경 사항을 관찰하십시오! 

<img src=images/github-dockerhub_15.jpg />


***

자신 만의 Hello Earth 컨테이너 응용 프로그램을 트위트에 올리십시오! 

>*참고 - tweet에서 &quot;사용자 이름&quot;이라고 적혀있는 Docker 허브 계정 이름을 사용하십시오.*

```
Check out my Hello Earth #Docker app that I just created in my #OracleCode HOL.  It's in my Docker Hub https://hub.docker.com/r/username/hello-earth
```


**축하합니다!** 이 실습 랩을 성공적으로 완료했습니다! 

***

## 참가자의 컨테이너를 보여주는 Oracle Container Cloud Service의 데모


Oracle Container Cloud Service에서 컨테이너 실행 체크 아웃 : 

*[Get Started for Free](https://cloud.oracle.com/tryit) 

***

## 추가 리소스에 대한 요약 / 요약 포인터


*[Get Started for Free](https://cloud.oracle.com/tryit) 

*[Oracle GitHub](https://github.com/oracle/docker-images) 

*[Oracle Images on the Docker Store](https://store.docker.com/search?q=oracle&source=verified&type=image) 

*[Oracle Container Registry](https://container-registry.oracle.com) 

오라클 블로그 : 

*[Oracle Container Cloud Service Docs](http://docs.oracle.com/en/cloud/iaas/container-cloud/index.html) 

*[Containers, Docker and Microservices](https://community.oracle.com/community/cloud_computing/containers-docker-and-microservices) 

**완료**