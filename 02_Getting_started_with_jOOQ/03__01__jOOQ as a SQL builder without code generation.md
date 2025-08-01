# 03-01 jOOQ as a SQL builder without code generation

#### 📘 코드 생성기 없이 jOOQ 사용하기

#### ➡️ [해당 내용 보기](https://www.jooq.org/doc/3.20/manual/getting-started/use-cases/jooq-as-a-sql-builder-without-codegeneration/)

---

### ✅ 전제: 코드 생성 없이도 사용 가능

* jOOQ는 **정적 스키마 기반 코드 생성기 사용을 권장**하지만, **동적 스키마** 환경이라면 코드 생성 없이도 사용 가능합니다.
* 이 경우, jOOQ는 **SQL 빌더 역할**만 하며, 다음 특징을 가집니다.

| 🎯 특징              | 💡 설명                                                 |
| ------------------ | ----------------------------------------------------- |
| 🧱 DSL 기반 AST 생성   | 문자열, 리터럴 등을 객체화하여 타입 안전한 AST(Abstract Syntax Tree) 구성 |
| ✂️ 코드 생성기 미사용      | 사전 스키마가 없거나 동적 SQL이 필요한 경우 유용                         |
| 🔁 실행 도구는 외부 사용 가능 | JDBC, JdbcTemplate, Apache DbUtils 등과 결합 사용 가능        |
| 🧪 바인드 변수 자동 생성    | 기본적으로 PreparedStatement 기반으로 SQL + 바인드 변수 구성          |

---

### 💡 예시 코드: SQL 빌더로 사용

```java
// DSL을 이용해 SQL AST 생성
Query query = create.select(field("BOOK.TITLE"), field("AUTHOR.FIRST_NAME"), field("AUTHOR.LAST_NAME"))
                    .from(table("BOOK"))
                    .join(table("AUTHOR"))
                    .on(field("BOOK.AUTHOR_ID").eq(field("AUTHOR.ID")))
                    .where(field("BOOK.PUBLISHED_IN").eq(1948));

// SQL 문자열과 바인드 값 분리 추출
String sql = query.getSQL();
List<Object> bindValues = query.getBindValues();

// 또는 바인드값 인라인 포함된 SQL 추출
String inlinedSQL = query.getSQL(ParamType.INLINED);
```

---

### 📚 참고할 만한 섹션

* **SQL Building**: jOOQ DSL로 SQL 작성하는 상세 가이드
* **Plain SQL**: 문자열 기반 테이블/컬럼 표현 사용법
* **Bind Values**: 바인드 변수 처리 및 인라인 전략 정리

---

### ✨ 핵심 요약

* **코드 생성기를 사용하지 않아도 jOOQ의 DSL은 유용**합니다.
* SQL 문자열 생성만 필요할 때 가볍게 활용 가능
* JDBC 기반 실행 로직과 결합하거나, Spring/DbUtils와 혼용도 가능
