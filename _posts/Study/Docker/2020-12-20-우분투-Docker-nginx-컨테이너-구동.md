---
layout: post
title: "[Ubuntu]Docker 이미지를 받아 컨테이너 구동하기"
categories:
  - Study
  - Docker
tags:
  - Docker
  - Ubuntu
  - Cloud
  - Nginx
created_at: 2020-12-20T21:12:00+09:00
modified_at: 2020-12-19T21:12:00+09:00
---

## Docker 컨테이너란?

------------------------------------------------------------

애플리케이션의 코드와 애플리케이션을 실행하는데 필요한 다른 프로그램들, 라이브러리, 설정 파일들이 패키징되어있는 실행환경이라고 할 수 있다.<br/>
*출처: [컨테이너란?](https://azure.microsoft.com/ko-kr/overview/what-is-a-container/)*

쉽게 말하자면 애플리케이션을 단독으로 동작하게 하는데 필요한 모든 구성요소가 포함되어 있기때문에 해당 컨테이너만 있으면 애플리케이션을 구동할 수 있다는 이야기이다.<br/>

## Docker 이미지란?

-----------------

컨테이너를 생성하고 구동하기 위한 snapshot이라고 할 수 있다. **docker run** 명령어를 통해 해당 이미지의 컨테이너가 생성이 되고 dockerfile에 작성된 대로 구동하게 된다.

이미지와 컨테이너를 git에 비유하자면 이미지는 소스코드, 컨테이너는 실제 구동되는 애플리케이션이라고 할 수 있을것 같다.
이미지도 git과 마찬가지로 버전관리가 가능하며, 도커 허브에 특정 시점의 이미지를 push하여 이미지를 저장하고 pull하여 내려받을 수 있다.

## Docker 이미지를 받아 nginx 컨테이너 구동해보기

-----------------------

aigaret 프로젝트는 다음과 같이 구성되어 있다.
![image-20201221155122936](../../assets/img/2020-12-20-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-nginx-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B5%AC%EB%8F%99/aigaret-구조.png)

이 중에서 가장 먼저 nginx컨테이너를 구동해보자.

1. nginx 이미지 pull 받기

   * pull 명령어를 통해 도커 허브에서 이미지를 받을 수 있다

     ```bash
     docker pull {repository 이름}/{이미지 이름}:{버전}
     ```

     ![image-20201220192402140](post_img/2020-12-20-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-nginx-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B5%AC%EB%8F%99/docker-pull.png)

   * 위 이미지에서 repository 이름을 생략했음에도 pull이 가능한 이유는 사람들이 주로 사용하는 이미지가 저장되어 있는 docker의 공식 repository인 library에서 먼저 찾아서 가져오기 때문이다.
   * 즉, library/nginx:latest와 동일하다.
   * 참고로 버전(tag)를 생략할 경우 default 는 :latest이다.
   * docker images 명령어를 통해 이미지를 확인해보면 pull이 완료된 것을 확인할 수 있다.

2. 컨테이너 생성하기

   * run 명령어를 통해 컨테이너를 생성할 수 있다.

     ```bash
     docker run -d -p {host 포트}:{컨테이너 포트} --name {생성할 컨테이너 이름} {이미지 이름}
     ```

   * 옵션 설명

     * -d: 컨테이너가 백그라운드에서 동작하도록 생성한다.
     * -p: 컨테이너와 host의 포트를 연결한다. aigaret 프로젝트를 위한 VCN설정시 http통신을 위한 80포트와 https통신을 위한 443포트를 개방하였으므로 nginx 컨테이너의 80포트와 443포트를 host의 포트와 연결한다.
     * --name: 생성할 컨테이너의 이름을 정한다. 옵션을 사용하지 않을 경우 랜덤으로 생성된다.

     ![image-20201220195547270](post_img/2020-12-20-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-nginx-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B5%AC%EB%8F%99/docker-run.png)

   * 잘 동작하는지 확인해보기

     ![image-20201220195945703](post_img/2020-12-20-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-nginx-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B5%AC%EB%8F%99/nginx-check.png)

     * curl {VM인스턴스 ip 주소}:80 명령어로 요청을 보낸 결과 응답이 잘 오는 것을 확인 할 수 있다.
     * 443의 경우 개방은 되어있지만 nginx에서 443 포트로 들어오는 요청에 대해 응답을 하고 있지 않기 때문에 설정을 통해 443포트로 들어오는 요청에도 응답하도록 셋팅해야한다. 아래는 리다이렉트로 응답하는지 확인만 할 수 있도록 설정해놓았다.

     ![image-20201220203648539](post_img/2020-12-20-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-nginx-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B5%AC%EB%8F%99/nginx-443-check.png)

