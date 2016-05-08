###### 비개발자를 위한 MySQL
# 기본 조건절

데이터를 가져올 때 목적에 맞는 데이터만을 가져와야합니다. 불필요한 데이터는 혼란을 야기할 수 있습니다. 이번 장에서는 **조건절**을 이용하여 필요한 데이터만을 가져오는 방법을 알아봅시다.

## WHERE?
SQL에서는 `WHERE`라는 조건절을 사용할 수 있습니다. `WHERE`말고도 `HAVING`, `ON` 등 여러 조건절이 있지만 지금은 아직 몰라도 되는 내용입니다. 이번 장에서는 `WHERE`에 대해서 집중적으로 알아봅시다.

## 사용법
```sql
SELECT * FROM table WHERE column > 10;
```
기본 형태는 위와 같습니다. 저번 SELECT 기초 장에서 본 것에서 크게 다르지 않습니다. 단지 `WHERE column > 10` 부분이 추가 되었을 뿐입니다. 위 형태에서 보듯이 `WHERE`는 무조건 `FROM`뒤에 위치해야 합니다. 예약어 위치는 [공식 문서](http://dev.mysql.com/doc/refman/5.7/en/select.html)에 자세히 나와있습니다. `WHERE` 뒤에 위치하는 `column > 10`은 하나의 **조건**을 의미합니다. 전체 문장을 해석해보면 `table 테이블에서 전체(*)을 선택하겠다. 단 column이 10 초과인 로우만`으로 해석 할 수 있습니다.

## AND, OR


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
