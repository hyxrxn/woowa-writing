# 프로덕션 코드 건드리지 않고 swagger 사용하기
### 작성자: 우아한테크코스 6기 백엔드 아토
### 작성일: 2024년 11월 15일

---------------

## 목차
1. API Docs
    1. API Docs란
        - API Docs에 대한 간단한 설명 및 사용 이유
    2. 대표적인 종류
        - Postman
        - Swagger
        - REST Docs

2. Swagger와 REST Docs 결합하기
    1. Swagger와 Swagger UI
        - 각각의 차이점
    2. REST Docs를 이용해 Swagger UI 사용하기
        - 과정 및 원리
        - 적용법
    3. 추가 팁
        - REST Docs 더 예쁘게 사용하기



--------

## 1.	API docs
### i. API Docs란?
개발자에게 문서란 떼 놓을 수 없는 존재다.
문서는 개발 과정에서 지식 공유와 협업을 원활하게 만들고, 코드의 유지보수성과 확장성을 높이는 필수적인 도구이기 때문이다.
그중 하나인 API Documentation(이하 API Docs)은 API의 여러 기능과 그 기능들의 사용법, 데이터 구조를 설명하는 문서다.
여기서 API는 Application Programming Interface의 약자로, 소프트웨어들이 서로 통신하고 데이터를 주고받기 위해 정의된 규칙과 메서드의 집합이다.
API Docs에서는 이 API를 어떻게 사용하고 호출해야 하는지, 각 요청과 응답의 형식이 무엇인지를 설명한다.
또한 각 에러 상황별로 전달하는 에러 코드와 그 의미도 설명한다.

API Docs를 사용하면 얻을 수 있는 이점은 다음과 같다.
가장 먼저, API Docs를 활용하면 개발자 간의 효율적인 커뮤니케이션이 가능해진다.
API를 사용하는 개발자들에게 각 엔드포인트(endpoint), 요청 메서드(GET, POST 등), 응답 형식, 전달해야 하는 파라미터 등을 명확히 알려줌으로써 오류를 줄이고 빠른 개발을 가능하게 한다.
또한 유지보수와 디버깅이 편리해진다.
문서화를 통해 API의 구조를 쉽게 파악할 수 있기 때문에 코드 수정과 및 문제 상황 파악이 쉬워진다.
그리고 API를 외부에 공개하는 경우, API Docs로 사용을 유도할 수 있다.
문서가 부족하면 구조를 이해하기 어렵기 때문에 사용을 꺼리게 된다.
잘 정리된 문서는 이해도와 신뢰도를 높이는 데 큰 도움이 된다.
마지막으로, 문서가 있으면 테스트 자동화가 용이하다.
API 테스트 툴과 연동하면 문서 기반으로 바로 테스트를 실행할 수도 있다.
따라서 더욱 편리한 검증을 진행할 수 있다.

그렇다면 이제 API Docs의 대표적인 종류와 각각의 사용법, 장단점을 알아보자.
사용법은 Spring Boot, Gradle 프로젝트 기반으로 설명한다.

### ii. 대표적인 종류
#### Postman
Postman은 API 개발 및 테스트에 쓰이는 대표적인 툴이다. 
주로 개발 진행 중에 사용한다. 
요청과 응답을 쉽게 주고받을 수 있어 이를 기반으로 결과물을 빠르게 확인할 수 있기 때문이다. 
추가적으로, 이를 기반으로 문서를 작성할 수 있는 기능도 제공한다. 
이 글에서는 이 문서 작성 기능을 위주로 설명한다.

- **사용법**
  1. Collections 탭에서 + 버튼을 눌러 새 컬렉션을 만든다. 

        <img width="379" alt="image" src="https://github.com/user-attachments/assets/6671e408-3789-47f6-aba5-26d509aaf2aa">

  2. 컬렉션 이름 우측의 세 점을 눌러 Add Request로 새 요청을 만든다. 

        <img width="375" alt="image" src="https://github.com/user-attachments/assets/8ddffde8-3061-4c21-9d89-176c450e3087">
  
  3. 서버를 실행하고, API 요청을 전송해 실제 서버로부터 응답을 받는다. 

        <img width="452" alt="image" src="https://github.com/user-attachments/assets/44d1f534-3a76-465f-8a68-e8e2408c76ce">
  
  4. 컬렉션 이름 우측의 세 점을 눌러 View documentation으로 컬렉션과 요청에 대한 설명을 적는다. 

        <img width="452" alt="image" src="https://github.com/user-attachments/assets/58503a9a-1a2f-478f-8ca2-d0e349503899">

  5. 우측 상단의 Publish 버튼을 눌러 추가 정보를 입력하고 문서를 생성한다. 문서는 링크를 통해 공유할 수 있다. 

        <img width="452" alt="image" src="https://github.com/user-attachments/assets/f7b2a36f-9690-4e81-9595-bc098fc50a40">
  
  6. 추가적으로 환경 변수를 설정할 수 있다.


- **장점**
  - UI가 직관적이고, 사용이 편리해 초보자도 쉽게 접근할 수 있다. 
  - 요청 및 응답 결과를 한눈에 확인할 수 있으며, 빠른 테스트가 가능하다. 
  - Team Workspace 기능을 통해 API 요청 및 문서를 팀원들과 공유하며 협업할 수 있다.


- **단점**
  - 자동화된 문서화보다는 수작업이 많이 필요해 대규모 API 문서 작성에는 적합하지 않다.


#### Swagger
Swagger는 API 문서를 표준화하여 정의하고, 이를 기반으로 자동화된 문서 생성을 돕는 툴이다.
최근에 Swagger의 스펙이 OAS(OpenAPI Specification)으로 통합 및 표준화되었다.
OAS는 API의 경로, 메서드, 요청 및 응답 구조를 명확히 정의하기 위해 JSON 또는 YAML 형식으로 작성되는 명세다.
애플리케이션을 실행하면 Swagger는 애노테이션을 통해 API 명세를 자동으로 생성한다.
이후 웹 기반의 UI로 API를 테스트할 수 있다.

- **사용법**
    1. 의존성을 추가한다.
    ```
    dependencies {
        implementation 'org.springdoc:springdoc-openapi-ui:1.7.0'
    }
    ```
    2. 어노테이션으로 API 명세를 정의한다.
        - @Operation: 각 엔드포인트의 제목과 설명을 정의한다. summary에 간단한 설명, description에 상세 설명을 적는다.
        - @ApiResponses: API의 응답 코드를 정의하며, 코드별 응답 메시지를 추가할 수 있다.
        - @Parameter: 요청 파라미터의 설명을 정의한다. Description에 각 파라미터에 대한 설명을 적을 수 있고, required에 필수 여부를 지정할 수 있다.
    ```java
    @Operation(summary = "사용자 정보 조회", description = "ID를 통해 특정 사용자의 정보를 반환합니다.")
    @ApiResponses(value = {
            @ApiResponse(responseCode = "200", description = "정상적으로 사용자 정보를 조회했습니다.", content = @Content),
            @ApiResponse(responseCode = "404", description = "해당 ID를 가진 사용자가 없습니다.", content = @Content)}) 
    @GetMapping("/{id}") 
    public String getUserById(@Parameter(description = "조회할 사용자의 ID", required = true) @PathVariable("id") Long id) { 
        return "특정 사용자 정보 반환";
    }
    ```
    3. 서버를 실행하고, `/swagger-ui.html` 경로로 문서를 확인한다.

        <img width="452" alt="image" src="https://github.com/user-attachments/assets/fe58ea1c-fb35-4128-9273-f44a00c1d5e4">
        <img width="452" alt="image" src="https://github.com/user-attachments/assets/34d79917-095e-4f07-824c-56c62963e57f">


- **장점**
    - 코드와 문서를 동기화하여, 코드에 변화가 생길 때마다 API 문서도 자동으로 갱신된다.
    - Swagger UI를 통해 직관적인 API 문서를 제공하고, 이를 이용한 테스트가 가능하다.
    - OAS를 기반으로 문서를 생성해 표준화된 형태의 문서화를 지원한다.


- **단점**
    - 코드가 변경되었을 때 어노테이션을 업데이트하지 않으면 코드와 문서 간 불일치가 발생할 수 있다.
    - 프로덕션 코드에 어노테이션을 추가하며 코드를 복잡하게 만들 수 있다. 이로 인해 가독성이 떨어질 수 있다.


#### REST Docs
Spring REST Docs는 Spring 프레임워크 기반의 애플리케이션에서 RESTful API 문서를 생성하는 툴이다.
테스트 코드를 기반으로 문서화하기 때문에 코드와 문서의 일관성을 유지할 수 있다.
Swagger와 달리 인터랙티브한 UI는 제공하지 않지만, 정확하고 신뢰할 수 있는 문서를 생성하는 데에 강점이 있다.

- **사용법**
    1. 의존성을 추가한다.
    ```
    dependencies {
        testImplementation 'org.springframework.restdocs:spring-restdocs-restassured:3.0.0'
        testImplementation 'io.rest-assured:rest-assured:4.4.0'
    }
    ```
    2. 테스트를 아래와 같이 설정한다.
    ```java
    @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
    public class ApiDocumentationTest {
  
        private RequestSpecification spec;
 
        @BeforeEach
        public void setUp(RestDocumentationContextProvider restDocumentation) {
            spec = new RequestSpecBuilder()
              .addFilter(documentationConfiguration(restDocumentation)
                    .operationPreprocessors()
                    .withRequestDefaults(prettyPrint())
                    .withResponseDefaults(prettyPrint())
              )
              .setPort(port)
              .build();
      }
    }
    ```
    3. 테스트를 작성한다.
    ```java
    @Test
    @DisplayName("게시글의 좋아요 여부를 조회한다.")
    void readLike() {
        RestAssured.given(spec).log().all()
                .filter(document(DEFAULT_RESTDOCS_PATH,
                        "특정 레시피의 좋아요 여부를 조회합니다.",
                        "레시피별 좋아요 여부 조회 API",
                        pathParameters(
                                parameterWithName("recipeId").description("레시피 아이디")
                        ),
                        responseFields(
                                fieldWithPath("isLike").description("나의 좋아요 여부")
                        )))
                .when().get("/likes/{recipeId}", 2L)
                .then().log().all()
                .statusCode(HttpStatus.OK.value())
                .body("isLike", is(true));
    }
    ```
    4. `./gradlew asciidoctor`를 실행하여 문서를 생성한다. 이 task는 Asciidoc 형식으로 작성된 내용을 기반으로 HTML, PDF와 같은 정적인 문서를 빌드하는 작업을 수행한다.


- **장점**
    - API 테스트와 문서화를 동시에 수행하여, 코드와 문서 간의 일관성을 유지하고 문서의 신뢰도가 올라간다. 
    - Spring 프레임워크와 긴밀히 연동되며, 프로덕션 코드에 영향을 미치지 않고 별도의 테스트 코드로 문서를 관리할 수 있다.


- **단점**
    - Swagger나 Postman에 비해 초기 설정이 까다롭고, 사용법을 익히는 데 시간이 걸릴 수 있다. 
    - Swagger처럼 웹 UI에서 문서를 바로 확인하고 테스트할 수 있는 기능이 없다. 
    - 문서화가 테스트 코드에 의존하기 때문에 API 테스트를 먼저 작성해야 한다.


#### 장단점 요약
| Tool      | 장점                                                                                                                                                       | 단점                                                                                                                                                 |
|:----------|:---------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|
| Postman   | - UI가 직관적이고, 사용이 편리해 초보자도 쉽게 접근할 수 있다.<br> - 요청 및 응답 결과를 한눈에 확인할 수 있으며, 빠른 테스트가 가능하다.<br> - Team Workspace 기능을 통해 API 요청 및 문서를 팀원들과 공유하며 협업할 수 있다.       | - 자동화된 문서화보다는 수작업이 많이 필요해 대규모 API 문서 작성에는 적합하지 않다.                                                                                                 |
| Swagger   | - 코드와 문서를 동기화하여, 코드에 변화가 생길 때마다 API 문서도 자동으로 갱신된다.<br> - Swagger UI를 통해 직관적인 API 문서를 제공하고, 이를 이용한 테스트가 가능하다.<br> - OAS를 기반으로 문서를 생성해 표준화된 형태의 문서화를 지원한다. | - 코드가 변경되었을 때 어노테이션을 업데이트하지 않으면 코드와 문서 간 불일치가 발생할 수 있다.<br> - 프로덕션 코드에 어노테이션을 추가하며 코드를 복잡하게 만들 수 있다. 이로 인해 가독성이 떨어질 수 있다.                                                                             |
| REST Docs | - API 테스트와 문서화를 동시에 수행하여, 코드와 문서 간의 일관성을 유지하고 문서의 신뢰도가 올라간다.<br> - Spring 프레임워크와 긴밀히 연동되며, 프로덕션 코드에 영향을 미치지 않고 별도의 테스트 코드로 문서를 관리할 수 있다.                 | - Swagger나 Postman에 비해 초기 설정이 까다롭고, 사용법을 익히는 데 시간이 걸릴 수 있다.<br> - Swagger처럼 웹 UI에서 문서를 바로 확인하고 테스트할 수 있는 기능이 없다.<br> - 문서화가 테스트 코드에 의존하기 때문에 API 테스트를 먼저 작성해야 한다. |


## 2.	Swagger와 REST Docs 결합하기
### i. Swagger와 Swagger UI
#### 각각의 차이점
- Swagger
    - API 명세(스펙)를 정의하는 도구와 라이브러리 모음이다.
    - RESTful API의 구조, 엔드포인트, 파라미터, 응답 등을 YAML 또는 JSON 포맷으로 작성한다. 
    - Swagger는 OpenAPI Specification(OAS)의 일종으로, API의 설계와 문서화를 위해 사용된다.
    - 이를 통해 개발자들이 API 인터페이스를 표준화된 방식으로 정의하고 공유할 수 있다.

- Swagger UI 
    - Swagger로 정의된 API 명세 파일을 시각화하여 웹 인터페이스로 표현해 주는 도구이다.
    - API 사용자나 개발자가 명세를 인터랙티브하게 탐색하고 테스트할 수 있게 해주며, 엔드포인트를 호출해 볼 수 있는 기능을 제공한다.

    
### ii. REST Docs를 이용해 Swagger UI 사용하기
#### 과정 및 원리
위에서 살펴보았듯, 사실 Swagger의 큰 장점인 웹 기반의 UI는 엄밀히 말해 Swagger가 아니다.
Swagger는 API 명세 작성 도구에 불과하고 그 결과물을 보여주는 인터페이스는 Swagger UI이다.
그래서 다른 도구로 Swagger UI가 이해할 수 있는 문서를 만든다면 Swagger의 불편함을 해결할 수 있다.
이를 이용하기 위해서는 Rest Docs를 이용해 문서를 작성하고 이를 Swagger UI가 이해할 수 있게 변환하면 된다.
이렇게 하면 Rest Docs의 장점인 높은 신뢰도를 가져갈 수 있고, 동시에 Swagger의 단점인 프로덕션 코드의 어노테이션을 제거할 수 있다.
또한 Swagger UI의 장점인 직관적인 문서 또한 유지할 수 있다.

#### 적용법
1. build.gradle 파일에 플러그인과 의존성을 추가한다.
```
plugins {
    id 'com.epages.restdocs-api-spec' version '0.18.2'
}

dependencies {
	testImplementation 'org.springframework.restdocs:spring-restdocs-restassured'
	testImplementation 'com.epages:restdocs-api-spec-restassured:0.18.2'
	testImplementation 'com.epages:restdocs-api-spec-mockmvc:0.18.2'
}
```
2. build.gradle 파일에 설정 블록과 task를 정의한다.
```
openapi3 {
	server = 'http://localhost:8080'
	title = 'Pengcook API'
	description = 'Pengcook API description'
	version = '0.1.0'
	format = 'yaml'
}

tasks.register("copyOasToSwagger", Copy) {
	dependsOn("openapi3")

	from layout.buildDirectory.file("api-spec/openapi3.yaml").get().asFile
	into "src/main/resources/static"
}

bootJar {
	dependsOn copyOasToSwagger
}
```
3. 위의 REST Docs 사용법을 따라 테스트를 설정하고 작성한다.
4. `copyOasToSwagger`를 실행하면 `openapi3.yaml`이 `resources/static`으로 들어온다.
5. 서버를 실행하고, `/swagger-ui/index.html` 경로로 문서를 확인한다.

### iii. 추가 팁
#### REST Docs 더 예쁘게 사용하기
- spec을 정의할 때, 여러 세팅을 할 수 있다.
  - 예를 들어, 필요 없는 헤더를 지울 수 있다.
```java
RequestSpecification spec = new RequestSpecBuilder()
        .addFilter(documentationConfiguration(restDocumentation)
                .operationPreprocessors()
                .withRequestDefaults(prettyPrint(), modifyHeaders()
                        .remove("Host")
                        .remove("Content-Length")
                )
                .withResponseDefaults(prettyPrint(), modifyHeaders()
                        .remove("Transfer-Encoding")
                        .remove("Keep-Alive")
                        .remove("Date")
                        .remove("Connection")
                        .remove("Content-Length")
                )
        )
        .setPort(port)
        .build();
```

- 상속을 통해 불필요한 중복을 지울 수 있다.
  - REST Docs를 위해 작성하는 컨트롤러 테스트 코드마다 spec의 정의가 중복되는 것은 불필요하다.
```java
@ExtendWith(RestDocumentationExtension.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public abstract class RestDocsSetting {

    protected static final String DEFAULT_RESTDOCS_PATH = "{class_name}/{method_name}/";

    protected RequestSpecification spec;
    @LocalServerPort
    int port;

    @BeforeEach
    void setUp() {
        RestAssured.port = port;
    }

    @BeforeEach
    void setUpRestDocs(RestDocumentationContextProvider restDocumentation) {
        spec = new RequestSpecBuilder()
                .addFilter(documentationConfiguration(restDocumentation)
                        .operationPreprocessors()
                        .withRequestDefaults(prettyPrint(), modifyHeaders()
                                .remove("Host")
                                .remove("Content-Length")
                        )
                        .withResponseDefaults(prettyPrint(), modifyHeaders()
                                .remove("Transfer-Encoding")
                                .remove("Keep-Alive")
                                .remove("Date")
                                .remove("Connection")
                                .remove("Content-Length")
                        )
                )
                .setPort(port)
                .build();
    }
}
```
