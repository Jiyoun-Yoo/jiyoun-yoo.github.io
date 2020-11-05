---
title: '1장 네트워크 첫걸음'
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Network-Basic
tag:
- Network-Basic
toc: true
toc_sticky: true
toc_label: Contents
description: 모두의 네트워크(길벗 출판사) 교재로 학습한 내용을 정리했습니다.
article_tag1: LESSON 01 네트워크의 구조
article_tag2: LESSON 02 정보의 양을 나타내는 단위
article_tag3: LESSON 03 랜과 왠
article_tag4: LESSON 04 가정에서 하는 랜 구성
article_tag5: LESSON 05 회사에서 하는 랜 구성
article_section: 네트워크
meta_keywords: 모두의 네트워크, network-basic
last_modified_at: '2020-10-01 22:00:00 +0800'
---

**'모두의 네트워크'** (길벗 출판사) 교재로 학습한 내용을 정리했습니다.

## LESSON 01 네트워크의 구조

### 1. 컴퓨터 네트워크란?
- **네트워크** : 연결되어 있는 상태
  - 네트워크는 컴퓨터 간의 연결 만을 말하는 것이 아니라, 사람과 사람의 네트워크, 도로와 철도의 네트워크, 물류 네트워크와 같이 다양한 네트워크가 있다.
- **컴퓨터 네트워크** : 컴퓨터 간의 네트워크
  - 네트워크를 통해 데이터를 서로 주고 받는다.
  - 컴퓨터가 한 대만 있으면 할 수 있는 일이 제한되지만, 컴퓨터가 여러 대 연결되면 컴퓨터 간의 데이터 파일 전송, 웹 사이트 열람, 메일 송수신과 같이 더 다양한 일을 할 수 있다.
- **인터넷** : 전 세계의 큰 네트워크부터 작은 네트워크까지를 연결하는 거대한 네트워크

### 2. 패킷이란?
- **패킷** : 컴퓨터 간에 데이터를 주고받을 때 네트워를 통해 전송되는 데이터의 작은 조각
- 큰 데이터가 있더라도 작게 나누어서 보내야 한다.
- 큰 데이터를 그대로 보내면 그 데이터가 네트워크의 대역폭을 너무 많이 차지해서 다른 패킷의 흐름을 막을 위험이 있다.
- **대역폭** : 일반적으로는 네트워크에서 이용 가능한 최대 전송 속도로 정보를 전송할 수 있는 단위 시간당 전송량을 의미
- 데이터를 패킷으로 분할하여 전송하는데,  패킷이 도착하면 번호 순으로 정렬하여 원래의 데이터대로 되돌리는 작업을 해야 한다.
- 예) 사진 파일 전송  
  먼저 사진 파일을 패킷으로 분할한다.
  순서 없이 도착하는 패킷을 순서대로 나열하여 원래 사진으로 만든다.

![패킷이란]({{ site.url }}{{ site.baseurl }}/assets/images/post/network-basic/이미지명.확장자){: .align-center}

## LESSON 02 정보의 양을 나타내는 단위

### 1. 비트와 바이트란?
- **디지털 데이터**
  - 모든 컴퓨터는 숫자 0과 1만을 다룬다. 그 0과 1의 집합을 디지털 데이터라 한다.
  - 0과 1의 정보를 나타내는 최소 단위를 **비트(bit)**라 한다.
  - 0과 1을 표현하는 1비트는 0 또는 1인 숫자 여덟개를 모아 표시할 수 있는데, 이 단위를 **바이트(byte)**라 부른다.
  - 8 bit  = 1 byte
  - 컴퓨터는 기본적으로 바이트 단위로 데이터를 읽고 쓰는 작업을 한다. 이 때, 모든 것을 0과 1의 집합으로만 다룬다.

![비트와 바이트]({{ site.url }}{{ site.baseurl }}/assets/images/post/network-basic/이미지명.확장자){: .align-center}

- **ASCII 코드**
- American Standard Code for Information Interchange
- 알파벳, 기호 , 숫자 등을 다룰 수 있는 기본적인 문자 코드  
  예) 문자 A → ASCII 코드 65
- 문자도 사진과 마찬가지로 상대방에게 숫자를 패킷으로 나누어서 전송하는데, 받은 쪽에서 패킷을 원래 값으로 되돌리는 작업을 한다.

![아스키 코드]({{ site.url }}{{ site.baseurl }}/assets/images/post/network-basic/이미지명.확장자){: .align-center}

## LESSON 03 랜과 왠

### 랜과 왠의 차이
- **랜(LAN)**
  - Locan Area Network(근거리 통신망)
  - 지리적으로 제한된 곳에서 컴퓨터와 프린터를 연결할 수 있는 네트워크
  - 한 공간 안에서 여러 대의 컴퓨터가 연결되어 있어도, 네트워크로 연결되어있으면 랜이라고 할 수 있다.

- **왠(WAN)**
  - Wide Area Network(광역 통신망)
  - 지리적으로 넓은 범위에 구축된 네트워크

![랜과 왠]({{ site.url }}{{ site.baseurl }}/assets/images/post/network-basic/ranwan.png){: .align-center} 




## LESSON 04 가정에서 하는 랜 구성
  
### 가정에서의 네트워크 구성

## LESSON 05 회사에서 하는 랜 구성

### 소규모 회사에서의 네트워크 구성