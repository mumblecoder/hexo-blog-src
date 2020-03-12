---
title: Socket - Packet
date: 2020-03-15 11:40:43
tags: [socket, packet]
categories: Socket
---

[참고글](https://brunch.co.kr/@wangho/6)

패킷통신상 데이터가 크거나 멀리서 오는 경우엔 분할되어 전달됨.
그럴땐 read를 여러번 해서 데이터를 합쳐야된다.
만약 2천바이트짜리 전문이 온다면 무식해보이더라도 반복문을 통해 2천번읽는게 가장 정확하다.
반복횟수를 줄이고 싶다면 한번에 읽는 바이트를 늘리면 되지만 그 길이만큼 못 읽었을때의 처리도 해줘야한다.

나의 경우엔 1441바이트와 나머지인 경우가 많아 1441 바이트로 잘라 읽었다.
전체길이가 1441보다 작을 경우엔 전체길이만큼 읽고, 1441이상이면 1441만큼 읽고 전체길이 - 1441 만큼 다시 읽었다.
```java
// 전문 헤더에 길이가 존재하여 그 값을 변수 telegramLength에 담았다
while(telegramLength > 0) { //헤더에 담긴 길이가 틀려서 음수가 될수도 있기에 >0으로 함.
  if(telegramLength >1441) {
	  log.info("==========1441 바이트 초과하여 분할 read==========");
	  telegramLength -= parsingBody(telegram, 1441);
  }else {
	  telegramLength -= parsingBody(telegram, telegramLength);
  }
	  sb.append(telegram.getBody()); // 분할하여 읽은 전문을 합치는 과정
}
if(telegramLength==0) {  
  telegram.setResultCode("OK");
}
```

예제 코드 넣고 패킷통신에 대해 추가 설명
