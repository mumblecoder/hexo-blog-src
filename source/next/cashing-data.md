자주 조회하는 정보들은 캐시 데이터로 저장해두고 가져다 쓰는게 디비가는일도 적고 빠르다고한다.
그 방법을 쓸때 자주 사용되는게 redis

나의 경우 Manager클래스를 만들어 놓고 서버 시작시 디비에서 가져와 맵객체에 저장하여 조회해서 쓴다.

어떤 데이터들을 캐시 데이터로 저장하는지 레디스는 어떻게 사용하는지 등에 대해서 공부해보자
