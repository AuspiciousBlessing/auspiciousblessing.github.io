---
layout: post
title: Web Server & Web Application Server
description: Web Application Server에 대한 고찰
date: 2024-10-21 02:50:00 +0900
categories: [Technical Concepts Summarized]
tags: [web server , web application server, was]
pin: false
math: false
mermaid: false
image:
  path: commons/webapp.png
  alt: HTTP(Hypertext Transfer Protocol)
---
<!-- categories: [Technical Concepts Summarized, Technical Labs, Technical Terms, Useful Apps To Help With Technology] -->

## Overview
Web Server라는 단어는 매우 포괄적인 단어로 크게는 하드웨어와 소프트웨어로 분류할 수 있고 소프트웨어 측면에서 보더라도 매우 포괄적입니다. 이 애매모호한 단어들 때문에 명확한 이해를 위해 정말 많은 시간을 들였습니다. 이번 포스팅에서는 소프트웨어 관점에서의 Web Server에 대해서 알아보겠습니다.

## Web Sever
Web Server는 웹 클라이언트로부터 들어오는 요청을 처리하고 웹 페이지, 이미지 또는 기타 멀티미디어 콘텐츠와 같은 요청된 리소스로 응답하는 소프트웨어 응용 프로그램입니다. Web Server는 World Wide Web의 중추로, 사용자가 인터넷을 통해 정보에 액세스하고 공유할 수 있도록 합니다.

Web Server는 클라이언트-서버 아키텍처를 사용하며, 서버 측 소프트웨어는 일반적으로 데이터 센터 또는 클라우드 컴퓨팅 환경에서 호스팅되는 전용 시스템에서 실행됩니다. 웹 브라우저와 같은 클라이언트 측 소프트웨어는 HTTP(Hypertext Transfer Protocol) 또는 HTTPS(HTTP Secure)와 같은 표준 프로토콜을 사용하여 서버 측 소프트웨어와 통신합니다.

Web Server는 일반적으로 여러 클라이언트의 많은 요청을 동시에 처리하는 데 최적화되어 있습니다. 자주 요청되는 콘텐츠를 캐싱하고, 여러 서버에서 요청을 로드 밸런싱하고, 데이터를 압축하여 네트워크 대역폭을 줄이는 등 성능과 확장성을 향상시키는 다양한 기술을 사용합니다.

일부 인기 있는 Web Server 소프트웨어에는 Apache HTTP Server, Nginx 및 Microsoft IIS(인터넷 정보 서비스)가 포함됩니다. 이러한 Web Server는 일반적으로 Linux, Windows 및 macOS를 포함한 다양한 운영 체제에 설치할 수 있는 오픈 소스 소프트웨어입니다.

Web Server는 HTML 페이지와 같은 정적 웹 콘텐츠와 PHP, Python 또는 Ruby와 같은 서버 측 스크립팅 언어로 생성된 동적 콘텐츠를 제공하는 데 사용됩니다. 이러한 서버 측 스크립트는 데이터베이스 또는 파일과 같은 서버 측 리소스에 액세스하고 클라이언트 요청에 대한 응답으로 동적 콘텐츠를 생성할 수 있습니다.

웹 콘텐츠를 제공하는 것 외에도 Web Server는 웹 애플리케이션 호스팅, 멀티미디어 콘텐츠 스트리밍 또는 다른 애플리케이션에 대한 API 서비스 제공과 같은 다른 목적으로 사용할 수 있습니다.

- 클라우드 기반 Web Server: 클라우드 기반 Web Server는 확장성, 유연성 및 비용 효율성으로 인해 점점 인기를 얻고 있습니다. 클라우드 기반 Web Server는 클라우드에서 호스팅되므로 기업은 필요에 따라 확장 또는 축소할 수 있으며 사용한 리소스에 대해서만 비용을 지불할 수 있습니다.
- 컨테이너화된 Web Server: Docker 또는 Kubernetes와 같은 컨테이너화된 Web Server는 여러 환경에서 웹 애플리케이션을 배포, 관리 및 확장할 수 있는 기능으로 인해 점점 더 대중화되고 있습니다.
- 서버리스 Web Server: AWS Lambda 또는 Azure Functions와 같은 서버리스 Web Server는 사용자가 기본 인프라를 관리할 필요 없이 수요에 따라 자동으로 확장할 수 있기 때문에 인기가 높아지고 있습니다.
- 마이크로서비스 아키텍처: 애플리케이션이 느슨하게 결합되고 독립적으로 배포 가능한 서비스의 모음으로 구축되는 마이크로서비스 아키텍처는 유연성, 확장성 및 복원력으로 인해 점점 더 인기를 얻고 있습니다.

또한 SSL/TLS 암호화, 방화벽 및 침입 탐지 시스템과 같은 보안 기능에 대한 강조가 증가함에 따라 Web Server의 보안이 강화되고 있습니다. 또한 Web Server는 사용자가 PHP, Python 또는 Ruby와 같은 다양한 서버 측 스크립팅 언어 중에서 자신의 필요에 가장 적합한 언어를 선택할 수 있도록 사용자 정의가 점점 더 가능해지고 있습니다.

또한 새로운 기술이 Web Server 기술의 환경을 변화시키고 있습니다. 다음과 같습니다.

엣지 컴퓨팅: 엣지 컴퓨팅은 일반적으로 네트워크 엣지에서 처리 능력을 사용자에게 더 가깝게 이동하는 것과 관련된 새로운 기술입니다. 이렇게 하면 웹 응용 프로그램의 성능을 개선하고 대기 시간을 줄이는 데 도움이 될 수 있습니다.
웹 어셈블리: 웹 어셈블리는 웹 브라우저에서 코드를 실행하기 위한 바이너리 형식으로, 개발자가 보다 강력하고 성능이 뛰어난 웹 애플리케이션을 만들 수 있도록 합니다.
인공 지능: 인공 지능(AI)은 사용자 행동을 예측하고 서버 응답을 최적화하여 Web Server 성능을 최적화하고 사용자 경험을 개선하는 데 사용됩니다.
블록체인: 블록체인 기술은 데이터가 중앙 집중식 서버가 아닌 분산된 노드 네트워크에 저장되는 분산형 웹 애플리케이션을 생성합니다.
웹 기술이 발전함에 따라 Web Server는 인터넷과 인터넷에서 실행되는 서비스 및 애플리케이션을 개발하는 데 중요한 역할을 할 것입니다. Web Server 관리의 새로운 기술과 모범 사례에 대한 최신 정보를 유지함으로써 조직은 Web Server 기술의 최신 혁신을 활용하고 사용자에게 최적의 경험을 제공할 수 있습니다.


## Web Server & Application Server
Web Server와 Application Server에는 서로 다른 독립적인 프로세스가 있습니다. 하지만 최종 사용자에게는 이 프로세스가 보이지 않습니다.

<img src="commons/static-webapp.png" alt="Device Mockup" style="margin-top: 50px; margin-bottom: 50px;" width="700" />

### Web Server 작동 방식
Web Server는 웹 사이트의 코드와 데이터를 호스팅하는 기술입니다. 브라우저에 URL을 입력할 때 이 URL은 실제로 Web Server의 주소 식별자입니다.

브라우저와 Web Server는 다음과 같이 통신합니다.

브라우저는 URL을 사용하여 서버의 IP 주소를 찾습니다.
브라우저는 정보에 대한 HTTP 요청을 보냅니다.
Web Server는 데이터베이스 서버와 통신하여 관련 데이터를 찾습니다.
Web Server는 HTTP 응답으로 HTML 페이지, 이미지, 비디오 또는 파일과 같은 정적 콘텐츠를 브라우저에 반환합니다.
그러면 브라우저가 정보를 표시합니다.
블로그, 헤더 이미지 또는 기사와 같은 정적 콘텐츠를 호스팅하는 웹 사이트를 Web Server에서 실행할 수 있습니다. 하지만 대부분의 웹 사이트와 웹 애플리케이션은 훨씬 더 대화형이기 때문에 Application Server가 필요합니다.

<img src="commons/dynamic-webapp.png" alt="Device Mockup" style="margin-top: 50px; margin-bottom: 50px;" width="700" />

### Application Server 작동 방식
Application Server는 동적 콘텐츠 생성, 애플리케이션 로직 및 다양한 리소스와의 통합을 지원하여 Web Server의 기능을 확장합니다. 애플리케이션 코드를 실행하고 메시징 시스템 및 데이터베이스와 같은 다른 소프트웨어 구성 요소와 상호 작용할 수 있는 런타임 환경을 제공합니다. 비즈니스 로직을 사용하여 Web Server보다 더 의미 있게 데이터를 변환합니다.

웹 사이트에서 대화형 콘텐츠에 액세스하려고 할 때 프로세스는 다음과 같이 작동합니다.

브라우저는 URL을 사용하여 서버의 IP 주소를 찾습니다.
브라우저는 정보에 대한 HTTP 요청을 보냅니다.
Web Server는 요청을 Application Server로 전송합니다.
Application Server는 비즈니스 로직을 적용하고 다른 서버 및 서드 파티 시스템과 통신하여 요청을 수행합니다.
Application Server는 새 HTML 페이지를 렌더링하고 이를 응답으로 Web Server에 반환합니다.
Web Server는 브라우저에 응답을 반환합니다.
브라우저가 정보를 표시합니다.
전자 상거래 웹 사이트를 예로 들면, 사용자는 장바구니에 항목을 추가하거나 물품을 결제할 때 Application Server와 상호 작용합니다.


## 주요 차이점: Web Server와 Application Server
Web Server와 Application Server에는 서로를 구분하는 몇 가지 주요 차이점이 있습니다.

- 다루는 태스크  
Web Server는 웹 사이트를 호스팅하고 간단한 요청에 대한 응답을 제공합니다. 또한 Web Server는 서버 활동을 기록하고 서버 측 스크립팅을 허용합니다.

  반면 Application Server의 태스크 세트는 더 복잡합니다. Application Server는 엔터프라이즈 시스템, 서비스 및 데이터베이스에 연결하여 동적 콘텐츠를 생성하는 비즈니스 로직을 처리합니다.

- 사용되는 프로토콜  
Web Server에 사용되는 기본 프로토콜은 HTTP 프로토콜입니다. 하지만 FTP와 Simple Mail Transfer Protocol(SMTP)을 지원하는 Web Server도 있습니다. 이 두 프로토콜은 파일 저장 및 전송과 이메일을 용이하게 합니다.

  Application Server는 Web Server에 사용되는 프로토콜 외에도 추가 통신 프로토콜을 사용하여 다른 소프트웨어 구성 요소와 통신합니다. 예를 들어 원격 메서드 호출(RMI) 및 원격 프로시저 호출(RPC)을 사용할 수 있습니다.

- 콘텐츠 유형  
Web Server는 대부분 정적 콘텐츠를 제공합니다. 정적 콘텐츠는 전송 전에 서버에서 수정하거나 처리할 필요가 없는 콘텐츠입니다. 예를 들어 이미지 파일(예: PNG, GIF 및 JPEG), 다운로드 가능한 문서(PDF), 비디오 및 HTML 파일은 모두 정적 콘텐츠입니다. 

  Application Server는 대부분 동적 콘텐츠를 제공합니다. 동적 콘텐츠는 사용자가 콘텐츠와 상호 작용하는 방식에 따라 변경되는 콘텐츠입니다. 예를 들어 동적으로 생성되는 보고서, 사용자 지정된 데이터 표현, 개인화된 UI, 데이터베이스 결과 및 처리된 HTML은 모두 동적 콘텐츠입니다.

- 멀티스레딩  
서버의 스레드는 태스크를 동시에 처리할 수 있도록 하는 별도의 작업 경로입니다. 멀티스레딩에서 서버는 여러 스레드를 동시에 생성하고 실행하며, 각 스레드는 별도의 태스크 또는 태스크의 일부를 처리합니다. 멀티스레딩이 지원되면 더 많은 웹 트래픽을 관리하면서 웹 콘텐츠를 더 빠르게 제공하는 데 도움이 됩니다.

  대부분의 Web Server는 멀티스레딩을 지원하지 않습니다. Web Server는 각각의 새 연결 요청을 대기열에 배치하고 이벤트 루프를 사용하여 대기열에서 새로 들어오고 나가는 요청을 모니터링합니다. 효율성을 높이기 위해 서버는 비차단 I/O 및 콜백을 사용하여 요청을 처리합니다. Web Server는 비차단 작업 및 이벤트 기반 아키텍처를 통해 동시 연결을 처리할 수 있습니다.

  Application Server는 멀티스레딩을 사용하여 높은 확장성과 효율성을 제공합니다. 요청에 외부 리소스가 필요한 경우 Application Server는 별도의 스레드를 사용하여 이러한 상호 작용을 처리합니다. 여러 스레드를 한 번에 처리하여 많은 클라이언트 상호 작용을 병렬로 처리할 수 있습니다. 


## Application Server와 Web Server는 어떻게 함께 작동하나
Application Server와 Web Server는 함께 작동하여 클라이언트 요청을 처리하고 사용자에게 올바른 콘텐츠를 제공합니다. 새 요청은 항상 Web Server에 먼저 수신됩니다. Web Server에서 정보 자체를 생성할 수 있는 경우 그렇게 한 다음 HTTP 응답을 다시 보냅니다. 또한 사용자가 요청한 데이터가 캐시에 이미 있지 않은지 확인합니다.

Web Server에서 사용자가 필요로 하는 콘텐츠에 액세스할 수 없는 경우 Web Server는 해당 요청을 Application Server에 전달합니다. 그러면 Application Server가 데이터를 처리하고 비즈니스 로직을 사용하여 올바른 정보를 제공합니다. 그런 다음 요청을 Web Server로 다시 전달하고, Web Server가 이를 사용자에게 전달합니다. 특정 아키텍처에서는 HTTP 요청을 자체적으로 처리하도록 Application Server를 구성할 수도 있습니다.


## Web Application Server
인터넷에서 Web Server와 WAS(Web Application Server)의 차이를 찾아보면 관련된 모든 포스팅 혹은 기사, 매거진에 기고된 글들에 동적 페이지를 생성하기 위해서는 모든 서버들이 Web Application Server가 당연히 필요한 것처럼 적혀있습니다. 하지만 현업에서 JAVA 진영 외에는 WAS라는 용어를 아예 쓰질 않습니다. Application Server라는 말은 포괄적으로 볼 때 간혹 쓰이기도 합니다만 세부적으로 언어 스택으로 볼 때는 이역시 쓰이지 않습니다. 저도 그래서 위에 WAS라고 쓰지 않았습니다.

WAS는 자바 진영에서만 쓰이는 용어인데 WAS를 마치 Application Server의 대명사인 것처럼 말하는 것은 사실 조금 무리가 있습니다. Application Server라는 용어는 자바 진영의 동적페이지를 생성하는.. 웹서버, 언어와 달리 따로 구성되어있는 서버라는 의미가 아니라 개념적인 설명에는 포괄적으로 웹을 만들어내는 서버 그 통째 혹은 웹서버와 구분해서 설명할 때는 비지니스 로직을 수행하는 서버를 칭합니다.

이렇게 생각해봅시다. 
PHP를 기반으로 하는 LAMP Stack에서 WAS 혹은 Application Server 무엇일까?
Python을 기반으로 하는 Python + Django + NginX세서 WAS 혹은 Application Server는 무엇일까?
NodeJS를 기반으로 하는 NodeJS + Express + NginX에서 WAS 혹은 Application Server는 무엇일까?

저도 여기서 의문이 제기되었고 Application Server라는 용어는 어떻게 생겨났고 Web Application Server라는 용어는 어떻게 생겨났을까? 왜 WAS는 자바 진영에서만 쓰일까 궁금했습니다. 대충 차이는 알고 답은 알지만 정확하게 이래서 이래하고 설명할 수는 없는 정도랄까요. 이 궁금증을 풀기 위해 수백개가 넘는 페이지들을 참조했습니다.


## Web Application Server 용어의 탄생
"WAS(Web Application Server)"라는 용어가 자바 생태계에서 주로 사용되고 다른 언어 생태계에서는 잘 쓰이지 않는 이유는, 역사적 및 기술적 차이에 기인합니다. 여기 몇 가지 이유를 설명하겠습니다:

1. 자바의 아키텍처와 복잡성
자바는 웹 애플리케이션을 실행하기 위해 여러 계층 구조를 요구하는 복잡한 아키텍처를 채택했습니다. 자바 Application Server는 JSP, Servlets, EJB(Enterprise JavaBeans) 등 다양한 기술 스택을 지원하며, 이러한 기술들은 웹 요청뿐만 아니라 트랜잭션 관리, 비즈니스 로직 처리, 데이터베이스 연동 등 복잡한 작업을 수행합니다.
이를 위한 서버들이 WAS라는 용어로 불리며, 고도의 복잡한 웹 애플리케이션을 위한 엔터프라이즈급 기능을 제공하는 서버 역할을 강조하기 위해 이런 용어가 사용됩니다.

2. 자바의 전통적 기업용 시장 지향
자바는 초기에 대기업에서 엔터프라이즈 애플리케이션을 구축하는 데 많이 사용되었습니다. 이러한 환경에서는 고급 기능을 제공하는 Application Server가 필요했기 때문에, WAS라는 개념이 자연스럽게 자리잡게 되었습니다.
Tomcat, WebSphere, WebLogic 등은 기업에서 복잡한 트랜잭션 관리와 고가용성 서비스를 제공하기 위해 설계된 자바 기반 Application Server입니다.

3. 파이썬과 PHP의 상대적인 경량성
파이썬과 PHP는 자바에 비해 상대적으로 더 단순하고 경량화된 웹 개발 스택을 제공합니다. 예를 들어, PHP는 아파치 서버에 모듈로 연동하여 작동하며, 별도의 복잡한 Application Server 없이도 쉽게 웹 애플리케이션을 배포할 수 있습니다.
파이썬의 경우, Flask나 Django 같은 프레임워크는 Web Server 게이트웨이 인터페이스(WSGI)라는 표준을 통해 서버와 연동되며, 자바의 WAS와 같은 대규모 환경보다는 상대적으로 단순한 개발 및 배포 환경을 지향합니다.
이로 인해 WAS 같은 복잡한 Application Server 개념이 불필요하게 되었고, 대신 Web Server(Apache, Nginx)나 Application Server(uWSGI, Gunicorn) 등의 용어가 사용됩니다.

4. 역사적 차이
자바 Application Server는 처음부터 J2EE(Java 2 Platform, Enterprise Edition)와 같은 대형 엔터프라이즈 애플리케이션을 위한 표준을 염두에 두고 발전해왔습니다. 반면, PHP나 파이썬은 더 가벼운 스크립팅 언어로 출발하여, 상대적으로 단순한 웹 개발 환경을 제공합니다.
따라서 자바는 처음부터 복잡한 애플리케이션을 위한 전용 서버(WAS)가 필요했지만, PHP와 파이썬은 별도의 Application Server 없이도 Web Server와 함께 잘 작동하도록 설계된 것입니다.

5. 기술적 표준 차이
자바는 JEE(Java Enterprise Edition)라는 규격을 따르는 WAS가 필요하며, 이는 자바 애플리케이션을 배포하고 실행하기 위한 특정 환경을 정의하고 있습니다. 반면, 파이썬이나 PHP는 그런 복잡한 표준 없이 작동하는 프레임워크와 서버를 사용하여 더 유연하게 개발할 수 있습니다.

## 자바 외 언어들의 WAS?
처음으로 돌아가서 Web Server는 정적 페이지만 서브가 가능하기 때문에 Web Application Server 혹은 Application Server가 따로 존재해야한다고들 했습니다. 그렇다면 자바가 아닌 다른 언어들은 어떻게 동적페이지를 생성할까요?

프로그래밍 언어라는 것은 단지 타이핑하는 문법만 존재하지 않습니다. 언어와 언어를 해석해주는 인터프리터가 함께 동봉되어있죠. PHP, Python, Javascript는 모두 인터프리터 언어로 인터프리터가 동적페이지를 생성합니다. 따라서 자바의 WAS처럼 따로 설치할 필요도 없죠. 때문에 Web Server와 프로그래밍 언어간에 통신이 필요합니다. JAVA의 경우 WAS가 JAVA와 Web Server 사이에서 통신을 해주는데 다른 언어는 WAS를 안쓰니까요. 그래서 Web Server와 통신하기 위해 Python은 WSGI(Web Server Gateway Interface)를 PHP는 mode_php, FastCGI, PHP-FPM 등을 사용합니다. 이들은 WAS가 아닙니다. 통신을 위한 프로토콜일 뿐 동적페이지를 생성하지 않으니까요.

<!-- https://aws.amazon.com/ko/compare/the-difference-between-web-server-and-application-server/ -->
<!-- https://www.ibm.com/kr-ko/topics/web-server-application-server -->
