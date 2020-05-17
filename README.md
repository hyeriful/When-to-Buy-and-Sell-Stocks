# When-to-Buy-and-Sell-Stocks
#### Termproject
---
### 데이터 획득
1. [한국거래소](http://www.krx.co.kr/main/main.jsp)에서 주식 회전율 상위 csv파일을 다운받는다.<br>
csv파일은 16,17,18대 각 대선 날짜 6개월 전부터 대선 당일까지 격일 단위로 다운받는다.
2. 상위 5위안에 드는 모든 기업들의 종가를 네이버 금융에서 web crawling을 통해 알아낸다.  
<br>

### 데이터 가공
(16, 17, 18대에서 모두 동일한 방법을 적용한다.)<br>

1. '데이터획득 1'에서 얻은  csv파일을 각각 읽어서 회전율 상위 5위 기업 정보를 가지고 있는 DataFrames을 만든다.
2. DataFrames에서 기업의 이름을 List에 저장한다.
3. List에 저장된 기업들을 검색하여(web crawling) '네이버금융 -> 일별시세' 에서 날짜마다 종가를 알아낸다. 기업명, 날짜, 종가를 가지고 있는 dictionary를 만든다.
4. 각 기업마다 종가의 최고가, 해당날짜, 종가의 최저가, 해당날짜를 알아내고 최고가가 최저가의 3배 이상인 기업들로만 구성되어 있는 dictionary를 만든다. key값은 기업명이고 value는 '최고가날짜, 최고가, 최저가날짜, 최저가'로 구성되어 있는 List이다.
5. '4'에서의 dictionary의 value값을 기반으로 날짜와 종가 관계 그래프를 그려본다.
6. 각 기업의 종가가 최고가, 최저가인 달(month)을 List에 저장해서 그 횟수를 통해 평균적으로 종가가 최고가인 달, 최저가인 달을 알아낸다.
---
#### 데이터 원본
1. 한국거래소에서 [회전율 상위 순위 정보](http://marketdata.krx.co.kr/mdi#document=040403) csv파일을 얻었다.<br>
csv파일을 18th_2012, 17th_2007, 16th_2002 폴더에 저장했다.
2. 웹크롤링을 위해 '네이버 금융에서 회사이름 검색->시세->일별시세' 페이지 소스코드를 살펴보다가 [일별시세 웹페이지](https://finance.naver.com/item/sise_day.nhn?code=047820) 발견했다(code는 회사별로 다름).
