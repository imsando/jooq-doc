# 03-03 jOOQ as a SQL executor

#### 📘 jOOQ 실행기로서의 활용

#### ➡️ [해당 내용 보기](https://www.jooq.org/doc/3.20/manual/getting-started/use-cases/jooq-as-a-sql-executor/)

---

### ✅ 전제: jOOQ를 직접 실행기로 사용하기

jOOQ는 SQL을 빌드하는 것뿐만 아니라, **직접 SQL을 실행(fetch/execute)** 하는 기능도 내장하고 있습니다.
이로 인해 DSL 기반 SQL 작성과 실행을 **하나의 API**로 연결할 수 있습니다.

---

### 💡 예시 1: DSL + 실행 통합

```java
// 타입 안전한 SQL을 작성하고 즉시 실행
Result<Record3<String, String, String>> result =
    create.select(BOOK.TITLE, AUTHOR.FIRST_NAME, AUTHOR.LAST_NAME)
          .from(BOOK)
          .join(AUTHOR).on(BOOK.AUTHOR_ID.eq(AUTHOR.ID))
          .where(BOOK.PUBLISHED_IN.eq(1948))
          .fetch();
```

* `fetch()` 호출 시 SQL이 실제 실행됨
* `Record[N]`로 결과 반환 → 컬럼 타입도 자동 추론됨

---

### 💡 예시 2: 외부 SQL 실행도 가능

jOOQ는 **순수 SQL 문자열**도 실행 가능합니다:

```java
// SQL 문자열 수동 구성
String sql = "SELECT title, first_name, last_name FROM book JOIN author ON book.author_id = author.id " +
             "WHERE book.published_in = 1984";

// 문자열 SQL 실행
Result<Record> result = create.fetch(sql);

// 또는 JDBC 결과셋으로부터 fetch
ResultSet rs = connection.createStatement().executeQuery(sql);
Result<Record> result = create.fetch(rs);
```

---

### 📚 참고할 만한 매뉴얼 섹션

* **SQL building**: jOOQ DSL로 SQL 작성하는 법
* **Code generation**: 스키마 기반 코드 자동 생성법
* **SQL execution**: jOOQ API로 SQL 실행하는 다양한 방식
* **Fetching**: `fetch()`, `fetchInto()`, `fetchOne()` 등 다양한 결과 추출법

---

### ✨ 핵심 요약

* jOOQ는 **SQL 빌드 + 실행까지 한 번에 처리 가능**
* DSL뿐 아니라 SQL 문자열, JDBC `ResultSet`까지 실행 대상이 됨
* fetch 결과는 타입 안전한 `Record[N]`로 제공되어 **실행-조회 일관성 확보**
