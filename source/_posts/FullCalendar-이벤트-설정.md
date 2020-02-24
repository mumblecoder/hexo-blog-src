---
title: FullCalendar 이벤트 설정
date: 2020-01-02 13:17:22
tags: [fullCalendar, javascript]
categories: MyProject
---

` 달력 출력은 했으니 이제 일정을 DB에서 받아 입력하고 여러 이벤트를 추가해보려고 한다.`

```javascript

document.addEventListener ( 'DOMContentLoaded', function () {	
  var calendarEl = document.getElementById('calendar');
  $.ajax({
    url: "/getSchedule",
    type: "get",
    success: function(result) {     //ajax로 DB에서 저장된 일정을 가져옴
      var calendar = new FullCalendar.Calendar(calendarEl, {
        plugins: [ 'interaction', 'dayGrid', 'timeGrid' ],
        defaultView: 'dayGridMonth',
   	events: result,                 //DB에서 가져온 데이터를 event로 넣어줌
        eventClick: function(info){     // 표시된 일정 클릭시 발생
          info.el.style.borderColor = 'red';   // 표시된 일정의 테두리선이 빨간색으로 바뀜
	  alert('View: ' + info.view.type);    // View: dayGridMonth 라고 알림창이 뜬다.
	},
	dateClick: function(info){      //일정 표시가 안된 날짜 부분 클릭시 발생
	  $("#add-modal").modal("show");  //모달창은 별도로 만들어놓은 상태
	  $("#start").val(info.dateStr);  // info.dateStr = 클릭한 부분의 
	  $("#end").val(info.dateStr);
	},
	defaultDate: new Date(),
	header: {
	  left: 'prev,next today',
	  center: 'title',
	  right: ''
	},
      });
      calendar.render();
    }
  });
});

```

function안에 들어간 **info** 객채에는 여러 속성값들이 있다.
FullCalendar 문서를 보면 알아보기 쉽게 잘 나와있다.
무튼 info 객체를 사용하면 원하는 이벤트들은 다 구현할듯하다.
