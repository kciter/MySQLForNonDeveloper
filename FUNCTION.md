###### 비개발자를 위한 MySQL
# 부록(함수)
이번 장에서는 MySQL에서 자주 사용되는 함수들을 소개하겠습니다.

## 숫자 처리 관련 함수

### `ABS`
절대값을 출력합니다.

사용 예:
```sql
SELECT abs(-100) FROM table;
# 결과
# 100
```

### `ROUND`
숫자를 반올림 합니다.

사용 예:
```sql
SELECT round(10.5) FROM table; # 자릿수를 생략하면 소수점 첫째 자리
# 결과 
# 11
SELECT round(12.5, -1) FROM table; # 자릿수는 0 또는 음수도 가능. 0이 소수점 첫째 자리를 의미함
# 결과
# 10
```

## 문자열 처리 관련 함수

### `CONCAT`
문자열을 이어줍니다.

사용 예:
```sql
SELECT concat(문자열1, 문자열2, 문자열3) FROM table;
SELECT concat("A", "B", "C") FROM table;
# 결과
# ABC
```

### `REPLACE`
문자열에서 바꿀 문자열을 바뀔 문자열로 치환합니다.

사용 예:
```sql
SELECT replace(문자열, 바꿀 문자열, 바뀔 문자열) FROM table;
SELECT replace("Lee Sun-Hyoup", "Sun", "Son") FROM table;
# 결과
# Lee Son-Hyoup
```

### `SUBSTRING`
문자열을 시작 위치에서 지정한 길이만큼 출력합니다.

사용 예:
```sql
SELECT substring(문자열, 시작위치, 길이) FROM table;
SELECT substring("Lee Sun-Hyoup", 4, 3) FROM table;
# 결과
# Sun
```

### `TRIM`
문자열 양쪽의 여백을 제거합니다.

사용 예:
```sql
SELECT trim(문자열) FROM table;
SELECT trim("  Lee Sun-Hyoup   ") FROM table;
# 결과
# Lee Sun-Hyoup
```

## 논리함수

### `IF`
논리식의 참, 거짓을 통해 값을 반환합니다.

사용 예:
```sql
SELECT if(논리식, 참 값, 거짓 값) FROM table;
SELECT if(1 = 2, 1, 2) FROM table;
# 결과
# 2
```

### `IFNULL`
첫번째 인자의 값이 NULL일 경우 두번째 인자의 값을 반환하고 NULL이 아닐경우 첫번째 인자의 값을 반환합니다.

사용 예:
```sql
SELECT ifnull(NULL, 2) FROM table;
# 결과
# 2
SELECT ifnull(1, 2) FROM table;
# 결과
# 1
```

## 집계함수

### `COUNT`
로우들의 갯수를 구하는 함수입니다.

사용 예:
```sql
SELECT count(*) FROM table;
# 결과
# 21
```

### `SUM`
로우들의 숫자 합을 구하는 함수입니다.

사용 예:
```sql
SELECT sum(value) FROM table;
# 결과
# 1004
```

### `AVG`
로우들의 숫자 평균을 구하는 함수입니다.

사용 예:
```sql
SELECT avg(value) FROM table;
# 결과
# 50
```

### `MAX`
로우들 중 가장 큰 값을 구하는 함수입니다.

사용 예:
```sql
SELECT max(value) FROM table;
# 결과
# 1000000000
```

### `MIN`
로우들 중 가장 작은 값을 구하는 함수입니다.

사용 예:
```sql
SELECT min(value) FROM table;
# 결과
# -2147383648
```

### `GROUP_CONCAT`
로우들의 문자열을 연결시켜주는 함수입니다.

사용 예:
```sql
SELECT group_concat(문자열) FROM table;
SELECT group_concat(value) FROM table; # value에는 각각 'A', 'B', 'C'가 들어가있다고 가정함
# 결과
# A,B,C
SELECT group_concat(value SEPARATOR ' ') FROM table;
# 결과
# A B C
```

## 날짜 처리 관련 함수

### `NOW`
현재 날짜와 시간을 출력합니다.

사용 예:
```sql
SELECT now() FROM table;
# 결과
# 2016-06-09 01:39:46
```

### `YEAR`
날짜의 년도를 출력합니다.

사용 예:
```sql
SELECT year('2016-06-09 01:39:46') FROM table;
# 결과
# 2016
```

### `MONTH`
날짜의 월을 출력합니다.

사용 예:
```sql
SELECT month('2016-06-09 01:39:46') FROM table;
# 결과
# 6
```

### `DAYOFMONTH`
날짜의 월별 일자를 출력합니다.

사용 예:
```sql
SELECT month('2016-06-09 01:39:46') FROM table;
# 결과
# 9
```

### `WEEKDAY`
날짜의 주별 일자를 출력합니다.

사용 예:
```sql
SELECT month('2016-06-09 01:39:46') FROM table;
# 결과
# 3
# (목요일)
```

### `DATE_FORMAT`
날짜를 지정한 형식에 맞춰서 출력합니다.

사용 예:
```sql
SELECT date_format('2016-06-09 01:39:46', '%Y/%c/%e %l:%i %p') FROM table;
# 결과
# 2016/6/9 1:39 AM
```

## 출처
http://egloos.zum.com/piccom/v/2866254

## 지적, 수정사항에 대해서
Github 계정이 있으신 분들은 Issue에 지적사항을 등록해주시거나 직접 수정하여 Pull request를 주시면 반영하도록 하겠습니다. <br>Github 계정이 없으신 분들은 kciter@naver.com를 통해 지적사항을 보내주세요. :smile:

## 라이센스
<a rel="license" href="http://creativecommons.org/publicdomain/mark/1.0/">
<img src="https://licensebuttons.net/p/mark/1.0/88x31.png" alt="Public Domain Mark" />
</a>

이 문서는 [CC0 라이센스](LICENSE)를 따릅니다.

특허권 또는 상표권은 CC0에 의해 영향을 받지 않으며, 퍼블리시티권 및 프라이버시권 등 저작물 자체에 대해 또는 저작물 이용에 대해 타인이 갖는 권리 또한 영향을 받지 않습니다.

달리 정하지 않은 한, 본 저작물의 인증자는 관련법에서 허용하는 최대 한도 내에서 저작물에 대해 아무런 보증도 하지 않으며 저작물의 모든 이용에 관한 어떠한 책임도 지지 않습니다.

저작물을 사용하거나 인용할 때 저자나 인증자로부터 승인을 받았다는 뜻을 시사하여서는 안됩니다.
