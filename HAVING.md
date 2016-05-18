###### 비개발자를 위한 MySQL
# 그룹 조건절

`WHERE` 명령어는 그룹으로 묶인 이후에는 적용되지 않습니다. `GROUP BY`로 묶이고 난 이후에 처리할 때는 `HAVING`이라는 명령어를 사용하게 됩니다. `HAVING`에 대해서 알아봅시다.

## `HAVING`
이번에는 조금 복잡한 조건을 가진 데이터를 가지고 오려고 합니다. 그 조건으로 각 손님의 주문 중 가격이 10,000원 이상인 것들의 합과 그 합이 100,000원 이상인 데이터만 가져오고 싶습니다. 그러면 다음과 같이 작성하면 될까요?

```sql
SELECT sum(price), customer FROM orders WHERE price >= 10000 AND sum(price) >= 100000 GROUP BY customer;
```

아쉽게도 위 쿼리는 동작하지 않습니다. `WHERE`의 조건은 **개별** 로우에 대해서만 동작합니다. 한 마디로 그룹화된 로우에 대해서는 동작하지 않습니다. 여기서 `HAVING`을 이용하게 되는데요, `WHERE`와 다르게 `HAVING`은 그룹화된 로우에 대해서만 동작합니다.

```sql
SELECT sum(price), customer FROM orders WHERE price >= 10000 GROUP BY customer HAVING sum(price) >= 100000;
# 결과
# sum(price)  |  customer
# 120000      |  이선협
# 151000      |  김지환
```

`HAVING`은 `GROUP BY`의 뒤쪽에 위치합니다. 위 쿼리를 설명하자면 전체 로우에서 **1차적**으로 `WHERE`를 통해 필터링합니다. 그 후 `GROUP BY`에 의해서 필터링된 데이터를 그룹화 한 후 `HAVING` 명령어를 통해 **2차적**으로 필터링됩니다. 그리고나서 데이터를 출력합니다. 즉 전체 로우 중 `price`가 10,000 이상인 데이터를 `customer` 기준으로 그룹화한 후 그 데이터에서 다시 sum(price)가 100,000 이상인 데이터만 가져오게 됩니다.

여기서 주의해야할 점이 있습니다. 위 쿼리에서는 조건에 `sum(price)`로 주었지만 이미 `SELECT`로 가져올 데이터에 속해 있을 경우 저러한 방식은 좋지 않습니다. `sum` 연산을 두번 하기 때문이죠. 이럴땐 어떻게 해결을 해야할까요?

## 별명
MySQL에서는 출력될 컬럼에 **별명**을 붙여줄 수 있습니다. 다음 쿼리를 봅시다.

```sql
SELECT count(*) as customers_count FROM orders;
# 결과
# customers_count
# 1234
```

결과의 컬럼 이름이 `customers_count`로 바뀌신 것을 보셨나요? 이처럼 출력될 컬럼의 이름을 지정해줄 수 있는데요, 이런 별명 붙이기를 통해 아까의 문제점을 해결할 수 있습니다.

```sql
SELECT sum(price) as price_sum, customer FROM orders WHERE price >= 10000 GROUP BY customer HAVING price_sum >= 100000;
# 결과
# sum(price)  |  customer
# 120000      |  이선협
# 151000      |  김지환
```

쿼리를 보시면 `sum(price)`의 별명을 `price_sum`으로 바꿔주고 `HAVING`절에서도 `price_sum`으로 바뀐 것을 볼 수 있습니다. 저런 방식으로 사용할 경우 두번 작업하지 않습니다.

## 마치며
이번 장에서는 `HAVING`과 별명에 대해서 배웠습니다. `HAVING`은 은근히 헷갈려 하시는 분들이 많은데요. 생각보다 어렵지 않습니다. 그리고 별명은 뒤에 서브쿼리와 `JOIN`을 배우게 되면 상당히 많이 사용하게 되는 문법입니다. 다음 장에서는 `distinct`에 대해서 알아보겠습니다.

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
