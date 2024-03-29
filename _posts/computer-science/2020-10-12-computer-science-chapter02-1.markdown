---
title: '컴퓨터 개론 2장 1절: 수의 체계와 변환(2진수)'
categories:
- Computer Science
tag:
- computer-science
description: 숭실대학교 글로벌미디어학부 정기철 교수님의 컴퓨터 개론 수업을 듣고 정리했습니다.
last_modified_at: '2020-10-12 23:00:00 +0800'
---

출처 : 숭실대학교 글로벌미디어학부 정기철 교수님의 컴퓨터 개론 수업을 듣고 정리했습니다.

---
# 1. 진법의 개념
- 고대 이집트의 숫자 표현 방법 (진법의 개념이 없을 때)

## 진법
- **유한한 심볼**로 **무한한 숫자**를 표현하는 방법  
  예) 10진법 : 0...9까지의 10개의 심볼로 무한한 숫자를 표현
- 사용할 수 있는 숫자 개수와 각 숫자의 위치 값을 정의한 수 체계
- 진법을 알아야 하는 이유
  - 컴퓨터는 0과 1, 디지털 형식으로 정보를 표현하는데, 이를 실생활에 적용하려면 아날로그 데이터를 디지털 데이터로 변환해야 함
  - 아날로그 데이터는 연속적인 데이터, 디지털 데이터는 비연속적인 데이터를 의미

## 서로 다른 진법 사용 예
- **천공 카드** : 2진법 (구멍이 뚫린 상태, 막힌 상태)
- **Pascal의 계산기** : 10진법 (톱니바퀴를 사용하는데 톱니 살이 10개)
- **ENIAC** : 10진법 (전자식으로 0 또는 1을 사용했지만 숫자를 표현할 때는 10진법을 사용, BCD 인코딩과 관련 있음)

# 2. 10진법과 2진법

## 10진법
- **0부터 9까지 10개의 숫자를 한 묶음**으로 하여 **10이 될 때마다 1자리씩** 자리를 올리는 방법
- '432'에서의 자릿수의 의미
  - 4는 432를 100으로 나누었을 때의 '**몫**'
  - 32는 앞서 100으로 나누었을 때의 '**나머지**'
  - 2는 10으로 나누었을 때의 '**나머지**'
- 컴퓨터는 0과 1, 두 가지 숫자로만 수를 표현하는 2진법을 사용
- 컴퓨터가 2진법을 사용하는 이유 : 최초의 컴퓨터가 진공관을 사용했기 때문인데, 진공관은 켜고 끄는(on/off) 기능만 있었기 때문에 진공관이 꺼지면 0, 진공관이 켜지면 1로 인식

## 컴퓨터 용량 단위
- **비트(Bit)** : 2진수를 표현하는 가장 기본 단위로, 데이터를 표현하는 최소 단위, 1비트는 0과 1의 2가지 상태만 표현 가능
- **바이트(Byte)** : 문자를 표현하는 단위로, 1바이트는 8비트를 하나로 모은 것, 1바이트는 256(=2^8)가지 상태를 표현 가능
- **워드(Word)** : 컴퓨터가 한 번에 처리할 수 있는 데이터의 단위로, 32비트 컴퓨터에서는 1워드는 4바이트

# 3. 진법의 변환

## 10진수 → 2진수
- **정수 계산 방식** : 10진수를 계속 2로 나누면서 몫은 아래에, 나머지는 오른쪽에 기입하면 됨, 몫이 더이상 2로 나누어지지 않을 때 아래에서부터 순서대로 나머지를 나열하면 2진수가 됨
- **소수 계산 방식** : 정부 부분은 위의 방식대로 변환, 소수점 아래의 소수 부분은 2를 계속 곱하면서 정수로 자리 올림이 발생하는지를 기록하고 이를 2진수 변환하면 됨

## 2진수 → 10진수
- **정수 계산 방식** : 2진수의 0과 1을 각 자릿수만큼의 2의 지수 승으로 곱한 후 모두 더하면 됨
- **소수 계산 방식** : 정수의 변환 방식과 동일하게 각 자릿수를 고려해 계산하면 됨, 단 정수와는 반대로 소수점 아래로 내려갈수록 자릿수가 커지고 마이너스를 붙여 계산해야 함

## 16진법
- 사람 입장에서는 2진법이 정확히 얼마인지 단번에 파악하기 어렵고 2진법을 표기하면 자릿수가 길어지기 때문에 편의상 16진법을 사용하기도 한다.
- 16진법으로 표현하려면 16가지 기호가 필요하다. A는 10진수의 10을 의미하고, F는 10진수의 15를 의미한다.
- **0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F**
- 2진법 → 16진법 변환 : 2진수의 오른쪽에서부터 4비트씩 모아 계산한다.
- 2진법 → 8진법 변환 : 2진수의 오른쪽에서부터 3비트씩 모아서 계산한다.

    