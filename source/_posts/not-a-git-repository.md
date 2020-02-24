---
title: not a git repository
date: 2019-12-17 15:38:01
tags: [git, hexo]
categories: hexo
---


`  어제에 이어 오늘도 포스팅을 하려고 git bash를 통해 git 명령어를 입력하니 not a git repository 라는 에러가 발생했다.`

not a git repository > 깃 저장소가 아니란 말이다.

우선 폴더안에 있던 .git 폴더가 사라졌다... 왜인지는 모르겠다...

어제까지는 잘만 되던게 왜 이러는지 모르겠지만 구글링을 시작!
<br>
구글링에 따르면 디렉토리 안의 .git 폴더를 삭제하고 git init 명령어를 실행하라고 한다.<br>
난 이미 없기에 바로 명령어를 실행했다.<br>
실행하니 .git 폴더가 생성되었고 블로그 세팅시 했던것 처럼<br>
` git remote add origin https://저장소주소` 실행하여 저장소 주소 연결해주고 <br>
` git remote -v` 실행하여 연결된 주소를 확인! <br>

그 후 나는 별생각없이 새 포스팅을 작성하고 push 하려고 했다. <br>
근데 push하려니 또 에러가 발생... ` failed to push some refs to ` <br>
구글링하니 원격저장소와 로컬저장소의 상태가 달라서 나는 에러라고 한다. <br>
push전에 pull을 먼저 했다면 에러가 안났을거란거! <br>
<br>
그래서 늦게나마 pull을 하려 했더니 새로운 에러 등장 ` refusing to merge unrelated histories ` <br>
git에서는 서로 관련 기록이 없는 두 프로젝트를 병합할때 거부하게 되어있다고 한다. <br>
```cs
git pull origin 브런치명 --allow-unrelated-histories
```

위의 명령어를 입력하면 병합하여 pull이 가능해진다. <br>

이후에는 별도 에러 없이 포스팅 가능~ <br>
끝!<br>
