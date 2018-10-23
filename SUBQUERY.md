###### 비개발자를 위한 MySQL
# 서브쿼리

서브쿼리는 **쿼리 안에 다른 쿼리가 들어가는 형태**를 말합니다.

직접 서브쿼리를 사용하는 것을 보면 더 쉽게 이해가 되니, 서브쿼리를 직접 보면서 배워봅시다.

## `SUBQUERY`
서브쿼리를 사용하기 위해 특별한 키워드를 쓰지는 않습니다. 다음과 같은 테이블이 있습니다.

|id |이름  |키   |친절함|
|---|------|-----|----|
|1  |김지환|185cm|100 |
|2  |장문익|182cm|99  |
|3  |이인재|190cm|80  |
|4  |이선협|168cm|0   |
|5  |신태민|170cm|85  |

여기서 친절함이 100인 사람의 이름을 알아보려고 합니다.

```sql
SELECT name FROM student WHERE id = (SELECT id FROM student WHERE kindness = 100 LIMIT 1);
# 서브쿼리의 결과가 1개라면 id = 으로 사용할 수 있지만, 2개 이상일 경우 오류가 발생합니다.
SELECT name FROM student WHERE id IN (SELECT id FROM student WHERE kindness = 100);
# 2개 이상의 서브쿼리 결과를 WHERE로 처리하기 위해선 IN을 사용합니다.
# 결과
# id  |  이름
# 1   |  김지환
```

위의 쿼리를 보면 **소괄호** 내부에 다시 쿼리가 나옵니다. 여기서 `SELECT name FROM student WHERE id =`을 **바깥 쿼리**, 그리고 괄호 안의 `SELECT id FROM student WHERE kindness = 100`을 **안쪽 쿼리**라고 부릅니다.

## 서브쿼리로 컬럼 추가하기
서브쿼리를 이용해 테이블에 존재하지 않는 **가상의 컬럼**을 추가 할 수 있습니다.
`student` 테이블에서 키 순서에 대한 컬럼을 추가해보도록 하겠습니다.

```sql
SELECT *, (SELECT count(*)+1 FROM student WHERE height > s.height) AS rank FROM student AS s;
# 결과
# id | 이름   | 키    | 친절함 | rank
# 1  | 김지환 | 185cm | 100    | 2
# 2  | 장문익 | 182cm | 99     | 3
# 3  | 이인재 | 190cm | 80     | 1
# 4  | 이선협 | 168cm | 0      | 5
# 5  | 신태민 | 170cm | 85     | 4
```

우리는 위 쿼리와 같이 서브쿼리의 결과에 대해 rank라는 별명을 붙이고 새로운 컬럼을 만들었습니다.

## 서브쿼리로 가상의 테이블 만들기
`SUBQUERY`는 `FROM`부분에도 들어갈 수 있습니다. 다음과 같은 테이블이 있다고 가정해봅시다.

|id |음식    |친절함|
|---|--------|------|
|1  |스테이크|100   |
|2  |파스타  |99    |
|3  |피자    |85    |
|4  |라면    |80    |
|5  |쑥      |0     |

```sql
SELECT * FROM (SELECT s.name, f.food FROM student AS s, foods AS f WHERE s.kindness = f.kindness);
# 결과
# id | 이름   | 음식     |
# 1  | 김지환 | 스테이크 |
# 2  | 장문익 | 파스타   |
# 3  | 이인재 | 라면     |
# 4  | 이선협 | 쑥       |
# 5  | 신태민 | 피자     |
```

위의 `FROM` 뒤의 안쪽 쿼리 `SELECT s.name, f.food FROM student AS s, foods AS f WHERE s.kindness = f.kindness`는 `student` 테이블과 `foods` 테이블에서 `kindness` 컬럼 값으로 두 테이블을 합친 쿼리입니다. (**다음 장에서 배울 JOIN 연산이 이런 작업을 합니다.**)

눈치 채신분도 계시겠지만 모든 `SELECT`를 통해 나온 결과는 이름없는 **가상 테이블**입니다. 이러한 가상 테이블도 `FROM`을 통해 데이터를 받아올 수 있습니다. 여기서 `AS`를 통해 별명을 붙여줘야 합니다.

## 마치며
이번 장에서는 `SUBQUERY`에 대해 알아보았습니다. 여기서 `SUBQUERY`는 수학적으로 단일 쿼리로 바뀔 수 있음이 증명되었고, `JOIN`을 사용한 쿼리로도 변경될 수 있으며 심지어 성능도 `JOIN`이 더 좋습니다. 하지만 서브쿼리를 쓰면 직관적이고 편하게 쿼리를 만들 수 있는 경우가 많습니다.

[다음 장](INNER-JOIN.md)에서는 `INNER JOIN`을 배워봅시다.

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
