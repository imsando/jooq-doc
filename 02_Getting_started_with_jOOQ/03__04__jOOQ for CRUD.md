# 03-04 jOOQ for CRUD

#### 📘 jOOQ를 활용한 CRUD 처리

#### ➡️ [해당 내용 보기](https://www.jooq.org/doc/3.20/manual/getting-started/use-cases/jooq-for-crud/)

---
### ✅ jOOQ의 CRUD 지원

jOOQ는 복잡한 쿼리 빌더뿐만 아니라, **일상적인 CRUD 작업(Create, Read, Update, Delete)** 도 간편하게 처리할 수 있습니다.

이 기능은 코드 생성기를 통해 생성된 `AuthorRecord`, `BookRecord` 등과 함께 사용할 때 특히 유용합니다.

---

### 💡 예시 코드: CRUD 흐름

```java
// READ: ID=1인 author 조회
AuthorRecord author = create.fetchOne(AUTHOR, AUTHOR.ID.eq(1));

// CREATE: 존재하지 않으면 새로 생성
if (author == null) {
    author = create.newRecord(AUTHOR);
    author.setId(1);
    author.setFirstName("Dan");
    author.setLastName("Brown");
}

// UPDATE: 'distinguished' 플래그 설정 후 저장
author.setDistinguished(1);

// SAVE: 존재하면 UPDATE, 없으면 INSERT
author.store();
```

* `fetchOne(...)`: 조건에 맞는 단일 레코드 조회
* `newRecord(...)`: 새 레코드 인스턴스 생성
* `store()`: DB에 저장 (INSERT or UPDATE 자동 처리)

---

### 📚 참고할 매뉴얼 섹션

* **SQL building**: DSL로 SQL 생성하는 법
* **Code generation**: 레코드/DAO/POJO 생성법
* **SQL execution**: `store()`, `delete()`, `fetchOne()` 등 실행 메서드

---

### ✨ 핵심 요약

* jOOQ는 **Record 객체를 통한 CRUD 조작**을 지원
* SQL DSL 없이도 `.store()`, `.delete()` 등으로 간단 처리 가능
* **ORM에 가까운 스타일**도 가능하지만, SQL 제어권은 여전히 개발자에게 있음
