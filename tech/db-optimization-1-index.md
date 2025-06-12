---
description: 인덱스란, 인덱스를 사용하면  좋은 경우, 인덱스를 타지 않는 경우
---

# DB 개선 ① - 인덱스

## 인덱스란

데이터베이스에서 검색 속도를 향상시키기 위해 사용되는 자료 구조

## 인덱스를 사용하면  좋은 경우

1. 검색(`SELECT` 연산)이 빈번한 경우
2. `INSERT`, `UPDATE`, `DELETE` 연산이 잘 일어나지 않는 경우
3. 카디널리티가 높은(중복이 적은) 컬럼에 생성하는 것이 유리
4. 단일 컬럼 여러개 생성 보다 다중 칼럼으로 좁은 인덱스 구성이 유리

## 인덱스를 타지 않는 경우

1.  함수를 적용하여 가공

    ex) `SUBSTRING` , `CONCAT` 등 사용
2.  부정형 비교

    ex) `NOT IN` , `!=` , `>` , `<`
3. &#x20;`LIKE` 문장의 전체 범위 지정
4. 인덱스 컬럼의 형변환

## 인덱스 관련 SQL

> 조회
>
> ```sql
> SHOW INDEX FROM tablename;
> ```

> 생성
>
> ```sql
> ALTER TABLE tablename ADD INDEX indexname (column1, column2, ...);
> ```

> 유니크 인덱스 추가
>
> ```sql
> ALTER TABLE tablename ADD UNIQUE INDEX indexname (column1, column2, ...);
> ```

> 삭제
>
> ```sql
> ALTER TABLE tablename DROP INDEX indexname;
> ```

> 📚 참고: 『개발자 기술 면접 노트』 – 이남희 지음
