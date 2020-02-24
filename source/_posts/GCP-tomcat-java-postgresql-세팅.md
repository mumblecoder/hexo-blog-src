---
title: GCP + tomcat + java + postgresql 세팅
date: 2019-12-17 14:50:21
tags: [GCP, tomcat, java, postgresql]
categories: MyProject
---

` 혼자 작은 프로젝트를 해보려고 하는데 현재 생각한 방식은 GCP + postgresql + SpringBoot 이다. 그 이유는 회사에서 쓰는 DB가 postgresql 이고 주로 부트에서 코딩을 한다. 서버는 뭘로 할까 하다가 GCP 크레딧 쓰던게 있길래 남은기간 그냥 써보기로...`

세팅하는데만 한참 걸렸다.<br>
멋모르고 이거저거 따라만 치다보니 별별 에러가 다 나왔다...<br>
생각나는대로 적어봐야겠다.<br>

기본적인 세팅은 회사에 서버세팅 문서가 있길래 따라했다.<br>
회사 자료라서 여기에 올려둘 순 없고 말로만 끄적여놔야겠다.<br>

먼저 GCP에는 우분투 18.04를 깔아두었고 터미널창을 통해 java1.8, tomcat9, postgresql10을 설치했다.<br>
관리한 디렉토리를 만들고 그룹과 유저를 만들어 디렉토리에 대한 권한을 부여했다.<br>

그 후 tomcat.service라는 파일을 만들었다. 아마 환경변수 등을 저장하는 설정파일? 같은거 인듯...<br>
그 다음 <br>
` sudo systemctl daemon-reload ` <br>
` sudo systemctl start tomcat `<br>
` sudo systemctl status tomcat `<br>
위 명령어를 입력하여 tomcat이 제대로 실행되었는지 확인했다.<br>

그 다음 postgresql<br>

설치 후 psql 명령어를 입력하면 쿼리를 쓸 수 있다. (그만 쓰려면 \q (저거 찾는데 한참걸렸다))<br>
유저를 생성하고 디비를 생성했다.<br>

이제 외부에서 DB를 관리하도록 연결을 하려했다.<br>
Pgadmin4를 사용하여 접속을 하려는데 timeout error...<br>
구글링 해보니 pg_hba.conf 파일과 postgresql.conf 파일을 수정해야했다.<br>
아래 링크로 가보면 캡쳐화면과 함께 설명이 잘 되어있다.<br>

참고 글 : https://dejavuqa.tistory.com/32

하지만 난 저렇게 해도 연결이 안됐다...<br>
그래서 구글링을 더 해본 결과 GCP에는 방화벽 설정을 해주어야 연결이 가능하다고 한다.<br>
그래서 포트번호 5432로 접근 가능하도록? 포트를 열어줬다고 해야하나?<br>
(해놓고도 말로 설명을 어떻게 해야할지 모르겠다...)<br>
무튼 방화벽까지 설정했더니 연결 성공~~~~ <br>

부트는 문서보고 기본 세팅은 한거 같은데 나중에 코딩한걸 올려봐야 확실히 알것 같다.<br>

오늘은 여기까지 끝!<br>


