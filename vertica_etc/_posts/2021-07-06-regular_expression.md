---
title:  "정규 표현식"
excerpt: "정규 표현식 입니다."
toc: true #heading 리스트 사이즈 바
toc_sticky: true #heading 리스트 사이즈 바 유지
categories:
  - vertica_etc
tags:
  - 정규 표현식
---

<script type="application/javascript">
function getIP(json){
    //dataLayer.push({"event":"ipEvent","clientIP":json.ip});
  clientIP = json.ip;

}
</script>

<script type="application/javascript" src="https://api.ipify.org?format=jsonp&callback=getIP"></script>


## 정규 표현식

**^ : 문자열의 처음을 나타냄**

|  식    | 문자열 |
|:-----:|:------------------|
|^group | group, groups, group program |

<br>


**$ : 문자열의 끝을 나타냄**

|  식    | 문자열 |
|:-----:|:------------------|
|ing$   | ing, sing, hosting, booting |
|^code$ | code |

<br>


**. : 임의의 한 문자**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
a.b | a와 b 사이에 한 문자가 낀 문자열 | aab, abb, acb |
ab. | ab 다음에 한 문자가 낀 문자열 | aba, abb, abc, |
a..b | a와 b 사이에 두 문자가 낀 문자열 | a11a, aabb, abbb, |
^.ape | ape 앞에 한 문자가 낀 문자열로 시작함 | tape, caper, |

<br>


***  : 바로 앞의 문자가 없거나 하나 이상이 있는 경우**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
|m*r | r 앞에 m이 없거나 하나 이상 있음 | r, mr, mmr, mmmr,|
|mr*s | m 다음에 r이 없거나 하나 이상 있고 s가 맨 뒤에 있음 | ms, mrs, mrrs, mrrrs,|
|mrs* | mr다음에 s가 없거나 하나 이상 있음 | mr, mrs, mrss, mrsss,|

<br>


**+ : 바로 앞에 문자가 하나 이상 있음**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
|m+r | r 앞에 m이 하나 이상 있음 | mr, mmr, mmmr|
|mr+s | m 다음에 r이 하나 이상 있고 s가 맨 뒤에 있음 | mrs, mrrs, mrrrs,|
|mrs+ | mr 다음에 s가 하나 이상 있음 | mrs, mrss, mrsss,|

<br>


**? : 0~1 회 나타나는 문자**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
|a? | a가 0~1회 등장하는 문자열 찾음 | ab, abc|

<br>


**[  ] : 문자 범위**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
|[w]s | s 앞에 w가 붙음 | ws|
|[ws]p | p 앞에 w나 s가 붙음 | wp, sp|
|[a-z]8 | 8 앞에 소문자 하나가 붙음 | a8, b8, c8, ···, z8|
|[a-zA-Z][0-9] | 로마자 하나 뒤에 숫자 하나가 붙음 | a0, b5, K3, ···|
|[^w]s | s 앞에 w가 아닌 문자 하나가 붙음 | as, 2s, es,  ···|
|[^ws]p | p 앞에 w나 s가 아닌 문자가 붙음 | ap, hp, op,  ···|
|[^a-z]8 | 8 앞에 소문자가 아닌 문자가 붙음 | A8, B8, 38, #8, ···|
|^[^gh][^ij]$ | g나 h가 아닌 한 문자로 시작하고 i나 j가 아닌 한 문자로 끝남 ( 대괄호 밖에 있는 ^는 문자열 처음) | ab, ty, ig, jh,  ···|

<br>


**{ } : 문자의 개수**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
|w{0}s | s 앞에 w가 없음 | s|
|w{0}s | s 앞에 w가 하나 붙음 | ws|
|ws{3}p | w가 앞에 오고 s가 3개 붙고 p가 뒤에 붙음 | wsssp|
|w{1,3}s | s 앞에 w가 1~3개 붙음 | ws, wws, wwws|
|w{,2}s | s 앞에 w가 두 개 이하 붙음 | s, ws, wws|
|w{2,}s | s 앞에 w가 두 개 이상 붙음 | wss, wsss,|

<br>


**\| : or  역할**

|  식    |     설명               | 문자열 |
|:-----:|:--------------------|:------------------|
|word \| phase  | word 또는 phrase  | word, phrase|
|mount(ed\|ing)  | mounted 또는 mounting | mounted, mouting|
|[^(a\|b\|c)].+ | a or b or c로 시작하지 않는 문자열 | describe,|

<br>


**\\ : 메타문자의 성분 없앨 때**

|  식    |     설명               | 문자열 |    안 맞는 문자열   |
|:-----:|:--------------------|:------------------|:------------------|
|\[[^\[\]]+\] | [   ] 으로 한 겹만 싸인 문자열 | [a], [ab], [abc],  ··· | [], [[abcd]], [a[]],  ···

