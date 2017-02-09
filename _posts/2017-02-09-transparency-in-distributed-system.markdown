---
layout: post
title: 분산 시스템에서의 Transparency
tags: [분산 시스템, Distributed system, Transparency]
comments: true
---

*아래 post는 Andrew S. Tanenbaum의 Distributed systems Principles and Pradigms 2nd edition을 참고하였습니다.*

## Abstract: 분산 시스템에서 Transparent가 무엇인가

분산 시스템은 보통 다음과 같이 정의된다.

> 분산 시스템은 사용자에게 단일 시스템처럼 보여지는 자율 컴퓨팅 요소들의 collection이다.

오늘 우리가 살펴볼 부분은 *단일 시스템처럼 보여지는* 이다. 분산 시스템은 여러 컴퓨터가 네트워크로 연결되어 공통된 task를 처리하는데 분산 시스템을 사용하는 user 입장에서는 이를 *하나의 시스템* 으로 인식한다. 그러한 **인식**을 위해서는 컴퓨터가 물리적으로 여러 위치에 흩어져있다는 사실을 **숨겨야** 한다. 이를 위해서 분산시스템에서는 **transparency** 를 정의하고 있다.

## *transpraent 의 종류*

    분산시스템의 여러 가지 측면을 transparent에 적용할 수 있다.
    resource나 process를 object라는 용어로 표현하겠다.

* Access transparency

    user가 resource에 access하고 그 resource가 representation 되는 방법들이 다름이 숨겨져야 한다.
    예로 remote file을 접근한다고 하면 그 방법은 local file 접근법과 같아야 한다.


* Location transparency

    user가 object가 physically 어디에 located 된 지 알 수 없다.
    Naming을 통해 이를 구현한다. 보통 이름에 logical 이름만 부여한다.

    주된 예시로는 URL이 있다. 예를 들어 `` http://dogfooter.github.io/index.html `` 이라는 URL이 주어진다면 user는 `` index.html ``에 대해서 정확히 서버 컴퓨터 어디에 위치한 지 알 수가 없다.

* Relocation transparency

    user가 시스템을 사용 중일 때 resource의 위치를 옮겨도 user는 알지 못한다.

* Migration transparency

    분산 시스템에서 resource에 어떻게 access 하는지 상관없이 resource는 옮겨질 수 있다.
    이를 migration transparency라 한다.
    즉 system에서 resource 혹은 process가 migration 해도 user는 알 수 없다.

* Replication transparency

    분산 시스템에서 resource의 availability 혹은 performance를 늘리기 위해서 resource를 replicate 해서(사본) 접근하기 쉬운 곳에 배치한다.

    이때 Replication transparency는 여러 사본의 resource가 있다는 것을 숨긴다.
    동시에 해당 resource가 다른 location에 있다고 하는 location transparency도 지켜져야 한다.

* Concurrency transparency

    data sharing 시에 다른 user가 같은 resource를 사용하고 있다고 인지하지 못하게 한다.
    중요한 점은 동시에 공유 데이터를 access 할 때 resource를 consistent state로 남겨야 한다는 것이다. consistent를 위해서는 locking 메커니즘을 사용해야 한다 이를 통해 원하는 데이터를 혼자 사용할 수 있다.

* Failure transparency

    user나 application이 system에 어떤 부분에서 failure가 발생해도 이를 알지 못하고, 시스템은 바로 해당 failure를 recover 한다.

    분산 시스템에서 failure를 숨기는 일은 매우 어렵다. recover가 어려운 주된 이유는 system 상에서 프로세스가 죽은 것인지 혹은 매우 느리게 반응하지 구분하는 게 사실상 불가능하기 때문이다. Web server를 예를 들면 user가 한 바쁜 web site를 접속할 때 결과적으로 browser에서 time out이 발생했다면 그 원인이 server가 죽은 것인지 혹은 네트워크가 매우 혼잡한지 할 수 없다는 것이다.

## 그러나

transparency를 지키기 위해서는 중요한 trade-off를 해야 한다. 앞서 설명한 failure transparency의 경우 매우 어려우므로 자칫하면 system 전체가 halt 하는 최악의 상황도 발생할 수 있다. 이는 부분적으로 숨기기 어렵다. 이러한 부분들은 다음 포스트에서 살펴보기로 한다.
