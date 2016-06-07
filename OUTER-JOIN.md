###### 비개발자를 위한 MySQL
# 외부 조인

각각의 테이블을 연결시켜주는 명령어는 서브쿼리와 내부 조인외에도 **외부 조인**이 있습니다. 내부 조인이 테이블 간의 교집합을 구해주는 반면, 외부 조인은 테이블 간의 **합집합**을 구해줍니다. 외부 조인에 대해서 알아봅시다.

## `LEFT JOIN`, `RIGHT JOIN`
외부 조인에는 `LEFT JOIN`과 `RIGHT JOIN`이 있습니다. 테이블을 왼쪽과 오른쪽에 두고 어떤 테이블을 먼저 가져올지 `LEFT`와 `RIGHT`로 정할 수 있습니다.

<p align="center">
  <img src="https://github.com/kciter/MySQLForNonDeveloper/blob/master/Images/img_leftjoin.gif?raw=true"><br>
  <sub><code>LEFT JOIN</code>은 왼쪽 테이블을 먼저 불러온다</sub>
</p>

위 그림이 조금 헷갈릴 수 있지만 `LEFT JOIN`은 왼쪽 테이블의 모든 데이터와 오른쪽 테이블과의 교집합 데이터를 불러올 수 있습니다.

<p align="center">
  <img src="https://github.com/kciter/MySQLForNonDeveloper/blob/master/Images/img_rightjoin.gif?raw=true"><br>
  <sub><code>LEFT JOIN</code>은 오른쪽 테이블을 먼저 불러온다</sub>
</p>

마찬가지로 `RIGHT JOIN`은 오른쪽 테이블의 모든 데이터와 왼쪽 테이블과의 교집합 데이터를 불러옵니다. 아직 감이 잘 안오시는 분들이 많을 것 같습니다.

예를들어, 이전에 봐왔던 주문 테이블과 손님 테이블을 `INNER JOIN`을 통해 불러올 경우 주문을 한 번도 하지 않은 손님의 데이터는 볼 수 없습니다. 하지만 `LEFT JOIN`과 `RIGHT JOIN`을 사용할 경우 주문을 한 번도 하지 않은 손님의 데이터(즉, 손님의 전체 데이터)와 주문을 한 번이라도 한 손님의 주문 데이터를 얻을 수 있습니다. `INNER JOIN`에서 사용했던 테이블을 통해 확인해봅시다.

<sub>주문 테이블</sub>

|id |손님id|메뉴id|손님이름|메뉴이름|가격 |
|---|------|------|--------|--------|-----|
|1  |12    |11    |이선협  |돼지고기|11000|
|2  |7     |25    |김려은  |육회    |9900 |
|3  |45    |81    |김지환  |연어회  |16000|
|4  |12    |91    |이선협  |소고기  |31000|

<sub>손님 테이블</sub>

|id |손님이름|키   |소지금|
|---|--------|-----|------|
|7  |김려은  |162cm|89900 |
|12 |이선협  |175cm|35000 |
|45 |김지환  |175cm|18000 |
|56 |윤명근  |170cm|10    |

여기서 윤명근은 한 번도 주문을 하지 않았습니다. 만약 여기서 `INNER JOIN`을 통하여 두 테이블을 연결할 경우 윤명근의 데이터를 볼 수 없습니다.

```sql
SELECT c.name, o.price FROM orders AS o
INNER JOIN customers AS c
ON o.customer_id = c.id;
# 결과
# c.name    |    o.price
# 이선협    |    11000
# 김려은    |    9900
# 김지환    |    16000
```

하지만 `LEFT JOIN` 혹은 `RIGHT JOIN`을 사용한다면 윤명근의 데이터도 볼 수 있습니다.

```sql
SELECT c.name, o.price FROM orders AS o
RIGHT JOIN customers AS c
ON o.customer_id = c.id;
# 결과
# c.name    |    o.price
# 이선협    |    11000
# 김려은    |    9900
# 김지환    |    16000
# 윤명근    |    NULL
```

하지만 이런 경우에 주문 데이터는 없기 때문에 `NULL`로 나타나게 됩니다.

## 과제

위 쿼리 결과에서 NULL을 안보이게 하려면 어떻게 해야할까요?

> 힌트: 함수

## 마치며
마지막으로 외부 조인에 대해서 배웠습니다. 다음 장부터는 부록입니다. 부록의 내용은 MySQL의 함수와 정규표현식, R프로그래밍 맛보기 입니다.

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
