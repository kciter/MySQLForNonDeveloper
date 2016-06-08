###### 비개발자를 위한 MySQL
# 부록(R프로그래밍 맛보기)
MySQL만으로는 언어적 한계로 인하여 원하는 데이터를 얻어내기 힘들 수 있습니다. 그럴때는 다른 언어를 이용하여 MySQL에서 얻어온 값을 조작하는 것이 더 편할 수 있습니다. 또한 차트와 같은 시각화를 해야한다면 MySQL로는 불가능합니다. 이번 장에서는 그런 문제점을 해결할 수 있는 데이터 시각화를 위한 R프로그래밍에 대해서 조금 맛보기를 해보겠습니다.

## 설치
설치는 [이곳](https://cran.r-project.org/bin/)에서 할 수 있습니다. OS에 맞춰서 설치하면 됩니다. 저는 Mac OS X이므로 Mac OS X에 맞춰서 진행하겠습니다.

## R 문법
R의 문법은 [이곳](http://tryr.codeschool.com/)에서 친절하게 배울 수 있습니다.

## MySQL 연동
R에서 MySQL을 이용하기 위해서는 **RMySQL**이라는 라이브러리를 설치해야 합니다. 설치 방법은 콘솔 창에서 `install.packages('RMySQL')` 명령어를 입력하면 설치됩니다.

간단한 사용법을 알아보겠습니다.

```r
install.packages('RMySQL') # RMySQL 라이브러리를 설치합니다.
library(RMySQL) # RMySQL 라이브러리를 불러옵니다.
con <- dbConnect(dbDriver("MySQL"), dbname = "DB이름", user = "root", password = "********")
# dbConnect 함수를 통해 MySQL에 접속합니다. con은 연결 객체입니다.
# dbname에는 데이터베이스의 이름을 입력합니다.
# user에는 유저 이름을 입력합니다.
# password에는 비밀번호를 입력해주세요.
result <- dbGetQuery(con, "SELECT * FROM table")
# dbGetQuery를 통해 SQL 쿼리를 전달할 수 있습니다. 그리고 그 결과는 result 변수에 저장됩니다.
result['id'] # 컬럼명을 통해 개별적으로 접근할 수 있습니다.
result[4, 'id'] # row, column
dbDisconnect(con) # MySQL과의 연결을 해제합니다.
```

사용법은 간단합니다. R을 이용하여 받아온 데이터를 처리할 수도 있습니다.

## 시각화
가져온 데이터를 처리한 후 시각화하는 방법에 대해서 알아봅시다.

```r
barplot(result[, 'price'])
# 너무 간단하네요
```

<img src='https://github.com/kciter/MySQLForNonDeveloper/blob/master/Images/r_chart.png?raw=true' width='400'>

`barplot`은 바 차트를 그리기 위한 R에서 제공하는 함수입니다. 이 함수를 이용하면 정말 간단하게 그래프를 그릴 수 있습니다.

R에는 다양한 라이브러리가 존재합니다. 기본적으로 제공하는 함수외에도 다양한 시각화 패키지가 존재합니다. 예를들면, 지도를 이용할 수도 있습니다.

## 결론
R을 이용하면 시각화가 가능합니다.

## 참고
* http://wsyang.com/2013/06/how-to-connect-r-with-mysql/

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
