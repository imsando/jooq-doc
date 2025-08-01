# 02-01 How to read this manual

#### 📘 jOOQ 매뉴얼 사용 가이드

#### ➡️ [해당 내용 보기](https://www.jooq.org/doc/3.20/manual/getting-started/the-manual/)

---

## 주요 키워드

| 🏷️ 구분                      | 📌 내용                                                                                   |
|------------------------------|--------------------------------------------------------------------------------------------|
| 💻 Code blocks               | SQL, Java, XML, 설정 파일 등 다양한 코드 블럭 예제가 제시됨                                       |
| 🔄 Code block contents       | SQL 코드와 jOOQ(Java DSL) 코드가 나란히 비교되며, 각 코드블럭은 Oracle 기준 등의 전제를 가짐               |
| ⚙️ Execution                 | jOOQ DSL에서는 `fetch()` 또는 `execute()`를 호출해야 쿼리가 실제로 실행됨 (즉시 실행되지 않음)            |
| ▶️ Degree (arity)            | jOOQ의 레코드는 1~22개의 컬럼을 가질 수 있으며, 이를 `Record[N]`, `Row[N]` 등의 형태로 표현함           |
| 🛠️ Settings                  | `org.jooq.conf.Settings`를 통해 런타임 동작을 커스터마이징 할 수 있으며, 명시가 없으면 기본값이 사용됨      |
| 🧪 Sample database           | 문서의 모든 예시는 jOOQ의 샘플 데이터베이스를 기반으로 하며, 이에 대한 설명은 별도 섹션에 있음             |


---

## \[1] 💻 Code blocks

* SQL, Java, XML, 설정 파일 등 다양한 코드 블럭을 사용해 예제를 제시합니다.
* 코드 블럭은 아래와 같은 형식을 포함합니다:

```sql
-- SQL
SELECT 1 FROM DUAL;
```

```java
// Java
for (int i = 0; i < 10; i++) { ... }
```

```xml
<!-- XML -->
<hello what="world"></hello>
```

```properties
# 설정 파일
org.jooq.property=value
```

---

## \[2] 🔄 Code block contents(SQL ↔ Java)

* SQL 코드와 jOOQ(Java DSL) 코드를 나란히 비교해 보여줍니다.
* 특별한 언급이 없을 경우 다음 전제를 따릅니다:

**SQL 전제**

* Oracle 문법 기준

**Java 전제**

* `DSL`은 `org.jooq.impl.DSL`에서 static import된 함수
* `create`는 `DSLContext` 인스턴스

**예시:**

```sql
-- SQL
SELECT 1 FROM DUAL;
```

```java
// Java
create.selectOne().fetch();
```

---

## \[3] ⚙️ Execution (기본 가정)

* PL/SQL, T-SQL과 달리 jOOQ는 즉시 실행되지 않음
* `fetch()` 또는 `execute()` 호출 시 실행됨

**예시:**

```sql
-- SQL
UPDATE t SET v = 1;
```

```java
// Java
create.update(T).set(T.V, 1).execute();
```

---

## \[4] ▶️ Degree (arity)

* jOOQ의 `Record[N]`, `Row[N]` 등은 컬럼 수를 의미함
* 1\~22개의 컬럼을 가진 레코드를 지원
* SQL 표준 용어인 "degree"를 사용

---

## \[5] 🛠️ Settings

* `org.jooq.conf.Settings`로 런타임 동작 설정 가능
* 설정이 명시되지 않으면 기본 설정 사용

```java
Settings settings = new Settings().withRenderFormatted(true);
DSLContext create = DSL.using(conn, SQLDialect.ORACLE, settings);
```

---

## \[6] 🧪 Sample database

* 문서의 예제는 샘플 데이터베이스를 기준으로 작성됨
* `BOOK`, `AUTHOR`, `FK_BOOK_AUTHOR` 등의 객체는 생성된 스키마에서 사용

