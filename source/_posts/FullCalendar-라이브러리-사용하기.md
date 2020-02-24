---
title: FullCalendar 라이브러리 사용하기
date: 2019-12-30 16:56:34
tags: [fullCalendar, javascript]
categories: MyProject
---

` fullCalendar를 사용하여 일정관리하는 기능을 넣으려고 한다. 학원다닐때도 한번쯤 써보고 싶었는데 이번기회에 써보기로!`

FullCalendar라고 검색하면 쉽게 찾아서 다운받을 수 있다.
나는 4.3.1을 다운받았고 압축을 풀어보면 package > core 파일이 있다.
그 안에 있는 main.js 파일과 main.css파일을 기본으로 넣어줘야하고 추가로 daygrid, timegrid파일의 main.js, main.css 그리고 interaction파일의 main.js 까지 넣어줬다.

` 본인 의지보다는 구글링하여 본 예시가 저렇게 넣었길래 따라 넣었... 필수 파일, 코드가 무엇인지는 아직 잘 모르겠다...`


아래는 fullcalendar를 적용한 자바스크립트 코드이다.

```javascript

document.addEventListener ( 'DOMContentLoaded', function () {
  var calendarEl = document.getElementById('calendar');		//HTML 부분에 id="calendar" 인 div 태그 만들어놈. 오타 조심!!!
  var calendar = new FullCalendar.Calendar(calendarEl, {
    plugins: [ 'interaction', 'dayGrid', 'timeGrid' ],    //이부분은 그냥 따라썼다.
    defaultView: 'dayGridMonth',                          //여기도
    eventSources:[{
    	events: [
	    	  {
	    		title : "test1",
	    		start : "2019-12-01",
	    		end : "2019-12-02"
	    	  },
	    	  {
	    	      title  : 'event2',
	   	      start  : '2019-12-05',
	    	      end    : '2019-12-07'
	    	  }
		],
		textColor: 'white'
    }],                           // 이벤트 소스 끝
    defaultDate: new Date(),
    fixedWeekCount: false,		// 보여주는 week수를 고정 할지 여부 (고정시 6주 비고정시 해당 달 주차만큼)
    aspectRatio: 1,				// 종횡비 (가로세로 비율)
    header: {
	      left: 'prev,next today',
	      center: 'title',
	      right: ''
	    },
  });
  calendar.render();
});

```

event는 달력에 표시할 일정들이다. 나중에 디비에서 가져올경우 저런형식으로 보내주면 잘 적용되어 보여지는거 같다.
eventSource의 경우 event외에 다른 속성들을 더 넣을라면 쓰고 아니면 event만 써도 된다.


Fullcalendar문서를 찾아보면 설명이 잘 되어있다.
[FullCalendar 문서](https://fullcalendar.io/docs)
문서보고 하나씩 테스트해보면서 프로젝트에 적용할 예정!

**적용화면**
![](/images/fullcalendar.jpg)

