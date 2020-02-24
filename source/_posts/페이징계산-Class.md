---
title: 페이징계산 Class
date: 2019-12-16 14:25:45
tags: [java, page]
categories: java
---

` 페이징 계산을 하려고 만든 클래스. 좋은건지는 모르겠지만 나중에 또 쓸거같아서 기록!`

```java
@Data
@FieldDefaults(level = AccessLevel.PRIVATE)  //lombok 사용
public class Paging {

	int total; 	 // 전체 게시글 수
	int page; 	 // 현재 페이지
	int totalPages;  // 총 페이지 수
	boolean next;    // 다음 페이지 여부
	boolean prev;    // 이전 페이지 여부
	int startPage;   // 시작 페이지
	int endPage;     // 마지막 페이지
	int pagePerNum;  // 한 페이지당 게시물 수
	int pagePerPage; // 보여줄 페이지 버튼 수
	
	
	public Paging(int page, int total) {
		this(page, total,10,5); // 한 페이지당 게시물 수, 보여줄 페이지 버튼 수를 넣지 않으면 기본 값은 10, 5
	}

	public Paging(int page, int total, int pagePerNum, int pagePerPage) {

		this.pagePerPage = pagePerPage;
		this.pagePerNum = pagePerNum;
		
		this.page = page;
		this.total = total;
		this.totalPages = total%pagePerNum==0 ? (total / this.pagePerNum): (total / this.pagePerNum +1);
		this.prev = (page==1? false : true);
		this.next = (page==this.totalPages ? false : true);
		
		if(page < this.pagePerPage/2 +1) {
			startPage = 1;
			endPage = pagePerPage>totalPages ? totalPages : pagePerPage;
		}else if(page > totalPages-this.pagePerPage/2){
			startPage = (totalPages +1 - pagePerPage) <1 ? 1 : (totalPages +1 - pagePerPage);
			endPage = totalPages; 
		}else {
			startPage = page - this.pagePerPage/2;
			endPage = page + this.pagePerPage/2;
		}
	}
}

```
