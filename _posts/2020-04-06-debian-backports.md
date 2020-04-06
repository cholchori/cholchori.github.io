---
title: Debian 최신버전으로 사용하기
layout: post
date: 2020-04-06
description: 
image: smile.gif
categories: ["IT"]
---

데비안은 안정성을 우선으로 하다 보니 패키지가 완전히 최신 버전은 아니다

지금 안정 버전인 Buster 도 커널이 4.19 버전이다

이런 패키지들을 최신으로 사용하기 위해 backports repositery 를 사용하면 된다 

백업을 받고

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

sources.list를 편집한다
```
deb http://deb.debian.org/debian buster-backports main
```

```
apt update
```
를 실행 한 다음

```
apt search linux-image
```
최신 버전 커널을 검색한다

너무 많이 나와 헷갈린다면

```
apt search linux-image | grep buster-backports
```
으로 검색해서

최신 버전의 linux-image 와 linux-headers 를 설치한다 
