---
title: Client-Server Model
description: About the client-server model
date: 2024-10-20 5:30:00 +0900
categories: [Technical Concepts Summarized]
tags: [Client, Server]
pin: false
math: false
mermaid: false
image:
  path: commons/Client-Server-Model.webp
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: client-server model
---
<!-- categories: [Technical Concepts Summarized, Technical Labs, Technical Terms, Useful Apps To Help With Technology] -->

클라이언트-서버 모델은 서버라고 하는 리소스 또는 서비스 제공자와 클라이언트라고 하는 서비스 요청자 간에 작업 또는 워크로드를 분할하는 분산 애플리케이션 구조입니다. 클라이언트-서버 아키텍처에서 클라이언트 컴퓨터가 인터넷을 통해 서버에 데이터 요청을 보내면 서버는 요청된 프로세스를 수락하고 요청된 데이터 패킷을 클라이언트로 다시 전달합니다. 클라이언트는 리소스를 공유하지 않습니다. 클라이언트-서버 모델의 예로는 EMAIL, World Wide Web 등이 있습니다.

## 클라이언트-서버 모델은 어떻게 동작할까?

- 클라이언트: 클라이언트라는 단어를 말할 때 특정 서비스를 사용하는 개인이나 조직에 대해 이야기 하는 것을 의미합니다. 마찬가지로 디지털 세계에서 클라이언트는 서비스 제공자(Server)로부터 정보를 수신하거나 특정 서비스를 사용할 수 있는 컴퓨터(Host)입니다.

- 서버: 서버라는 단어에 대해 이야기할 때 그것은 무언가에 봉사하는 사람이나 매체를 의미합니다. 마찬가지로 디지털 세계에서 서버는 정보(데이터) 또는 특정 서비스에 대한 액세스를 제공하는 원격 컴퓨터입니다.

그래서, 그것은 클라이언트가 무언가를 요청하고 서버가 데이터베이스에 있는 한 그것을 제공합니다.

## 브라우저가 서버와 상호 작용하는 방식
클라이언트 서버와 상호 작용하기 위해 따라야 할 몇 가지 단계가 있습니다.
- 사용자가 웹 사이트 또는 파일의 URL(Uniform Resource Locator)을 입력합니다. 
- 브라우저는 DNS(Domain Name System) 서버에 URL에 대한 IP 주소를 질의합니다.
- DNS 서버는 요청한 URL에 할당된 웹서버의 IP 주소로 응답합니다. 
- 브라우저는 HTTP/HTTPS 요청을 웹서버의 IP로 보냅니다.
- 서버는 요청된 파일을 클라이언트로 보냅니다.
- 브라우저는 서버로 부터 받은 파일을 렌더링합니다. 이 렌더링은 DOM(Document Object Model) 인터프리터, CSS 인터프리터 및 JIT(Just in Time) 컴파일러로 통칭되는 JavaScript 엔진의 도움으로 수행됩니다.

![Device Mockup](commons/Client-Server-Model-2.png){: w="700" }

## 클라이언트-서버 모델의 장점
- 모든 데이터를 한 곳에 모은 중앙 집중식 시스템.
- 비용 효율성으로 유지 보수 비용이 적고 데이터 복구가 가능합니다.
- 클라리언트와 서버의 용량은 별도로 변경할 수 있습니다.

## 클라이언트-서버 모델의 단점
- 클라이언트는 바이러스, 트로이 목마 및 웜이 서버에 존재하거나 서버에 업로드 되는 경우 취약합니다.
- 서버는 DOS(Denial of Service) 공격에 취약합니다.
- 데이터 패킷은 전송 중에 스푸핑(Spoofing)되거나 수정될 수 있습니다.
- 사용자의 로그인 자격 증명 또는 기타 유용한 정보를 피싱하거나 캡처하는 것이 일반적이며 MITM(Man in the Middle) 공격이 일반적입니다.

## 결론
클라이언트-서버 모델은 제어 및 보안을 강화하기 위해 서버의 리소스를 통합하고, 유연한 클라이언트 옵션을 허용하며, 확장성과 효율성을 위해 강력한 네티워크에 의존합니다. 비용에 대한 영향이 있기는 하지만 클라이언트-서버 모델은 여전히 기본적이며 클라우드 컴퓨팅 시대에 부합합니다.
