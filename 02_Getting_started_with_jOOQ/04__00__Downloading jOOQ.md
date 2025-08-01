# 04-00 Downloading jOOQ

#### 📘 jOOQ 다운로드 및 의존성 설정

#### ➡️ [해당 내용 보기](https://www.jooq.org/doc/3.20/manual/getting-started/getting-jooq/)

---

## 🔽 배포 채널

jOOQ는 다음 3가지 경로를 통해 배포됩니다.

1. **ZIP 파일 다운로드**: [https://www.jooq.org/download/versions](https://www.jooq.org/download/versions)
2. **상용 에디션 저장소 (Commercial only)**: [https://repo.jooq.org](https://repo.jooq.org)
3. **Maven Central (오픈소스 에디션 전용)**: [https://repo1.maven.org/maven2/org/jooq](https://repo1.maven.org/maven2/org/jooq)

---

## 📦 ZIP 파일 구성

웹사이트에서 받은 ZIP 파일에는 다음이 포함됩니다.

* `maven-install.sh / .bat` : 로컬 Maven 저장소에 설치
* `maven-deploy.sh / .bat` : Maven 원격 저장소에 배포

ZIP 파일에는 오픈소스 에디션 최신 버전 + 상용 에디션 전체 히스토리 포함됨 (스냅샷 포함)

---

## ☁️ Maven 저장소 접근 (상용 에디션용)

**settings.xml:**

```xml
<server>
    <id>jooq-pro</id>
    <username>[your licensee email]</username>
    <password>[your license key]</password>
</server>
```

**pom.xml:**

```xml
<repositories>
  <repository>
    <id>central</id>
    <url>https://repo1.maven.org/maven2/</url>
  </repository>
  <repository>
    <id>jooq-pro</id>
    <url>https://repo.jooq.org/repo</url>
  </repository>
</repositories>
```

---

## 📌 의존성 예시 (Maven)

```xml
<dependency>
  <groupId>org.jooq</groupId> <!-- 또는 org.jooq.pro 등 에디션에 맞게 -->
  <artifactId>jooq</artifactId>
  <version>3.20.5</version>
</dependency>
```

> 🔹 상용 에디션은 Maven Central에 없음 → ZIP으로 설치하거나 repo.jooq.org 사용
> 🔹 Java 버전별 그룹 ID가 다름 → 예: `org.jooq.pro-java-17`, `org.jooq.trial-java-11` 등

👉 [JDK 지원 매트릭스 보기](https://www.jooq.org/download/support-matrix-jdk)
