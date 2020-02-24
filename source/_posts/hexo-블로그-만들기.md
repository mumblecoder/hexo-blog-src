---
title: hexo 블로그 만들기
date: 2019-12-13 17:25:29
tags: [hexo, blog]
categories: hexo
---

Hexo를 사용하여 Blog를 만들려고 며칠동안 삽질을...
결국 icarus 테마를 적용한 Hexo 블로그를 만들었다!
지킬을 사용할때와는 달리 블로그 환경? 까지 깃에 저장해두어야 다른 컴퓨터에서도 편하게 쓸 수 있는거 같아서 설정 관련된걸로 고생했다...
무튼 틈틈히 삽질한 끝에 이제 초기 설정은 익힌듯!

이제 마크다운을 사용하여 글쓰는법에 익숙해져야겠다

지금부터는 마크다운 테스트 글

[마크다운 사용법 참고 글](https://heropy.blog/2017/09/30/markdown/)

**글자 양 끝에 `**`을 붙히면 bold 효과**

# 샵 1개
## 샵 2개
### 샵 3개
#### 샵 4개
##### 샵 5개
###### 샵 6개

` 양끝에 백틱 `

```sql
SELECT *
FROM temp
WHERE seq IS NOT NULL
```

```java
System.out.println("퇴근하고싶다");
```

```javascript
 var none = "none";
```

```html
<div class="temp">마크다운 익히기</div>
```

```css
.temp{
      border : solid 1px lightgray;
      background-color : black;
}
```

| 번호 | 이름 | 성별 |
|---|:---:|---:|
| `1` | Jack | M |
| `2` | Joo  | M |

>인용문 표시
>_출처_

수평선 그릴땐 - 또는 * 또는 _ 를 3번씩 입력
---
***
___

줄바꿈을 하고 싶을땐 `<br> 또는 띄어쓰기 2번`


