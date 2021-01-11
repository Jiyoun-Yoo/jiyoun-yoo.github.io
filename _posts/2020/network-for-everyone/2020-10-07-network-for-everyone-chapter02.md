---
title: '[모두의 네트워크] 2장 네트워크의 기본 규칙'
categories:
- network
tag:
- 모두의 네트워크
last_modified_at: '2020-10-07 22:00:00 +0800'
---

**'모두의 네트워크'** (길벗 출판사) 교재로 학습한 내용을 정리했습니다.

---
# LESSON 06 네트워크의 규칙
## 프로토콜이란?
- **통신을 하기 위한 규칙**을 프로토콜이라고 한다.
- 불어를 못하는 한국인과 한국어를 못하는 프랑스인이 서로의 언어로 대화를 시도한다면, 말이 통하지 않는다. 이럴 경우, 영어로 대화한다는 규칙을 정해서 대화할 수 있다.
- 편지를 배송하기 위해서는 편지를 쓸 때부터 상대방에게 도착할 떄까지 '편지를 쓰는 규칙', '편지를 보내는 규칙', '우체국의 규칙' 등 **서로 영향을 주지 않고 독립적인** 여러 규칙을 거쳐야 한다.

---
# LESSON 07 OSI 모델과 TCP/IP 모델
## 1. OSI 모델이란?
- OSI 모델은 네트워크 기술의 기본이 되는 모델이다. ISO라는국제 표준화 기구에서 OSI 모델이라는 표준 규격을 제정했다.
  - **ISO** : International Organization for Standardization(국제 표준화기구)
  - **규격** : 기술적인 사항에 대해 재정한 기준을 말하는데 보통은 기술적 표준을 의미

### OSI 모델의 7계층
- 컴퓨터에서 컴퓨터로 데이터를 전송할 때 컴퓨터 내부에서는 여러가지 일을 하는데, 이런 일을 일곱 개 계층으로 나누어서 한다.
- 이 때 그 일곱 개 **계층**이 아래의 그림과 같은 OSI 모델이다. 계층 대신 **레이어**라는 용어를 사용하기도 한다.

![OSI 모델]({{ https://jiyounyou.github.io/ }}{{ site.baseurl }}/assets/images/post/network-for-everyone/OSI-model1.png){: .align-center}{: width="60%" height="60%"}
- 통신할 때 데이터는 맨 위의 응용 계층에서 순차적으로 아래 계층으로 전달된다.

### 7계층에 대한 설명
![OSI 모델]({{ https://jiyounyou.github.io/ }}{{ site.baseurl }}/assets/images/post/network-for-everyone/OSI-model2.png){: .align-center}{: width="100%" height="100%"}

- 데이터를 전송하는 쪽(**송신 측**)은 데이터를 보내기 위해서 상위 층에서 하위 층으로 데이터를 전달한다.
- **각 계층은 독립적**이므로 데이터가 전달되는 동안에 다른 계층의 영향을 받지 않는다.
- 데이터를 받는 쪽(**수신 측**)은 하위 계층에서 상위 계층으로 각 계층을 통해 전달된 데이터를 받게 된다.
![OSI 모델에서 데이터 송수신]({{ https://jiyounyou.github.io/ }}{{ site.baseurl }}/assets/images/post/network-for-everyone/OSI-model3.png){: .align-center}{: width="80%" height="80%"}

## 2. TCP/IP 모델이란?
### TCP/IP 모델의 4계층
- TCP/IP 모델은 4계층으로 이루어져 있다.
- 각 계층에는 다양한 프로토콜이 있다.
![TCP/IP 모델]({{ https://jiyounyou.github.io/ }}{{ site.baseurl }}/assets/images/post/network-for-everyone/TCP-IP-model1.png){: .align-center}{: width="70%" height="70%"}

### OSI 모델과 TCP/IP 모델 비교
- OSI 모델의 응용 계층, 표현 계층, 세션 계층이 TCP/IP 모델에서는 응용 계층으로 합쳐져 있다.
![TCP/IP 모델]({{ https://jiyounyou.github.io/ }}{{ site.baseurl }}/assets/images/post/network-for-everyone/TCP-IP-model2.png){: .align-center}{: width="80%" height="80%"}

---
# LESSON 08 캡슐화와 역캡슐화
## 1. 캡슐화와 역캡슐화란?
### 캡슐화
- 데이터를 보내려면 데이터의 앞부분에 전송하는 데 필요한 정보를 붙여서 다음 계층으로 보내야 하는데, 이 정보를 **헤더**라고 한다.
- 헤더에는 **데이터를 전달받을 상대방에 대한 정보**도 포함되어 있다.

![캡슐화]({{ https://jiyounyou.github.io/ }}{{ site.baseurl }}/assets/images/post/network-for-everyone/capsulation.png){: .align-center}{: width="80%" height="80%"}
- 이처럼 헤더를 붙여나가는 것을 **캡슐화**라 한다.

### 역캡슐화
- 데이터를 받는 쪽에서는 헤더를 하나씩 제거해야 하는데, 이것을 역캡슐화라고 한다.