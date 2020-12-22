---
layout: post
title: "[Ubuntu]Docker 컨테이너 볼륨 설정하기"
categories:
  - Study
  - Docker
tags:
  - Docker
  - Ubuntu
  - Cloud
created_at: 2020-12-22T15:56:00+09:00
modified_at: 2020-12-22T15:56:00+09:00
visible: true
---

## Docker 볼륨이란?
---
컨테이너에는 애플리케이션이 동작하기 위한 모든 실행환경이 셋팅되어 있다.<br/>
또한 애플리케이션이 동작하면서 생성되는 것들(mysql에서는 data, nginx에서는 log 등)또한 컨테이너 안에 저장이 된다.<br/>

![image-20201222152718375](../../assets/img/2020-12-22-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-mysql-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EB%B3%BC%EB%A5%A8-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/컨테이너.png)

만약, 컨테이너의 업데이트, 오류 등으로 인해 컨테이너 삭제 후 다시 run 하게 된다면 이런 자료들이 컨테이너 삭제 시 모두 날아가기 때문에 반드시 백업이 필요하다.<br/>

![image-20201222153142327](../../assets/img/2020-12-22-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-mysql-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EB%B3%BC%EB%A5%A8-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/볼륨미지정.png)

이때 좀 더 편리하게 사용할 수 있는 것이 볼륨이다.<br/>
docker가 설치되어 있는 host pc의 디렉토리와 컨테이너의 디렉토리를 공유하여 컨테이너 삭제 시에도 볼륨 안의 자료가 host pc에 남아있게 된다.

![image-20201222153325483](../../assets/img/2020-12-22-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-mysql-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EB%B3%BC%EB%A5%A8-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/볼륨지정.png)



## Docker 볼륨 설정

---

1. 먼저 mysql 이미지를 pull 한다.
2. 배포 서버와 테스트 서버에서 저장되는 값을 HOST PC(여기서는 VM 인스턴스)와 공유하기 위한 디렉토리를 생성한다.

![image-20201222153838099](../../assets/img/2020-12-22-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-mysql-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EB%B3%BC%EB%A5%A8-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/볼륨디렉토리생성.png)

3. 아래 명령어로 mysql 컨테이너를 구동한다

   ```bash
   $ docker run -d -p {HOST PC 포트번호}:{컨테이너 포트번호} -v {HOST PC 디렉토리 경로}:{컨테이너 디렉토리 경로} -e MYSQL_ROOT_PASSWORD={설정하고싶은 mysql root password} --name {컨테이너 이름} {이미지 이름}
   ```

   * -v: 볼륨 설정을 위한 옵션
   * -e: 환경변수 설정을 위한 옵션 {이름}={값}으로 설정 가능

4. HOST PC에 볼륨 지정한 경로에 가서 파일을 하나 만들어준다.

   ![image-20201222154802798](../../assets/img/2020-12-22-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-mysql-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EB%B3%BC%EB%A5%A8-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/볼륨확인1.png)

5. 컨테이너에 접속해서 확인해보자.

   ![image-20201222154915057](../../assets/img/2020-12-22-%EC%9A%B0%EB%B6%84%ED%88%AC-Docker-mysql-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EB%B3%BC%EB%A5%A8-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/볼륨확인2.png)

   이렇게 HOST PC와 컨테이너 간의 볼륨설정이 된것을 확인 할 수 있다.