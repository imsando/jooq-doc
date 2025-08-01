# 03-02 jOOQ as a SQL builder with code generation

#### 📘 코드 생성기를 활용한 jOOQ DSL 사용

#### ➡️ [해당 내용 보기](https://www.jooq.org/doc/3.20/manual/getting-started/use-cases/jooq-as-a-sql-builder-with-code-generation/)

---

### ✅ 전제: 코드 생성기와 함께 쓰는 SQL DSL

jOOQ는 **SQL 빌더**로도 훌륭하지만, **코드 생성기**를 함께 사용하면 더 큰 시너지를 얻을 수 있습니다.

| 🎯 장점                | 💡 설명                                                   |
| -------------------- | ------------------------------------------------------- |
| 🔐 타입 안정성            | 존재하지 않는 테이블/컬럼 사용 시 컴파일 타임 오류 발생                        |
| 🧾 정적 구조 보장          | DB 구조에 기반한 Java 클래스 자동 생성 (`BOOK.TITLE`, `AUTHOR.ID` 등) |
| 📦 DSL + 타입 + 스키마 통합 | SQL 작성과 DB 구조 간 동기화 유지                                  |

---

### 💡 예시 코드: 코드 생성기 기반 DSL

```java
Query query = create.select(BOOK.TITLE, AUTHOR.FIRST_NAME, AUTHOR.LAST_NAME)
                    .from(BOOK)
                    .join(AUTHOR)
                    .on(BOOK.AUTHOR_ID.eq(AUTHOR.ID))
                    .where(BOOK.PUBLISHED_IN.eq(1948));

// SQL 추출 (PreparedStatement용)
String sql = query.getSQL();
List<Object> bindValues = query.getBindValues();

// SQL + 값 인라인 추출
String inlineSQL = query.getSQL(ParamType.INLINED);
```

* 기본적으로 바인드 변수(`?`) 사용됨 → JDBC, Spring JdbcTemplate, DbUtils 등에서 활용 가능

---

### 🧾 관련 매뉴얼 섹션

* **SQL building**: DSL 기반 SQL 작성법
* **Code generation**: 개발 DB 스키마 기반 Java 코드 생성 방법
* **Bind values**: 바인드 값의 관리 및 인라인 처리 방식

---

### ✨ 핵심 요약

* jOOQ 코드 생성기를 사용하면 **정적 타입 안정성** 확보
* SQL을 **IDE 자동완성 + 컴파일 시 검증** 가능
* JDBC, Spring, MyBatis 등 외부 실행 도구와도 잘 결합됨
