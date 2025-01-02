# Java Spring 프로젝트 개발 가이드
1.개발 환경  
IDE: IntelliJ IDEA 2024.2.4 (Community Edition), eclipse, vscode  
강력한 코드 편집기와 디버깅 도구를 제공하여 Spring 개발에 최적화  
Spring Initializr: https://start.spring.io/  
의존성관리 : maven, gradle  
Spring Boot: 3.3.5  
선택 항목:  
Spring Web  
Spring Data JPA  
H2  
Lombok  
DevTools  
Thymeleaf  
Java: 17 (LTS 버전)  
최신 기능과 안정성을 제공하는 장기 지원 버전입니다.  
https://jdk.java.net/17/ (openjdk)  
이 부분 수정  
2.프로젝트 구성
기본적으로 제공되는 index.html이 없을 경우 404 에러 발생
404 에러 처리:
resources/static/error 폴더에 404.html 추가하여 사용자 에러 페이지 제공
index.html 생성하여 기본 페이지 설정
Controller 생성: Thymeleaf를 사용하여 동적 페이지 접근 확인
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Welcome to Thymeleaf!</h1>
    <p th:text="${attribute}"></p>
</body>
</html>
Thymeleaf는 HTML을 서버에서 동적으로 렌더링합니다.
데이터베이스 연결
관계형데이터베이스(h2, mysql, postgresql), nosql(mongoDb) /SQL학습필요/
H2 데이터베이스 설정: application.properties에 다음 추가
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
기본 데이터 입력
프로젝트 실행 시 초기 데이터를 자동으로 입력하기 위해 아래 생성
( data.sql, schema.sql )
프론트엔드 기술
https://brunch.co.kr/@ourstellar/12
기술 스택: HTML, CSS, JavaScript, Vue.js (SPA 개발) /웹기초 html,css,javascript 학습필요/ /SPA프레임워크 학습하면 좋음/
Bootstrap: 웹사이트 화면 개발을 위한 프레임워크
기본 템플릿 Bootstrap 넣기
https://getbootstrap.kr/
서버 측 템플릿 엔진
JSP: 전통적인 엔진.. Spring Boot와 Thymeleaf의 호환성이 더 좋음
Freemarker
Thymeleaf: 동적 콘텐츠 렌더링에 적합하며, HTML5와 호환성이 좋음
https://www.thymeleaf.org
사용방법 :
<html xmlns:th="http://www.thymeleaf.org" >
<!-- <a class="navbar-brand" href="#!">Start Bootstrap</a> -->
<a class="navbar-brand" href="#!" th:text="${attribute}" >Start Bootstrap</a>
기본 적인 기능 /spring학습필요/
MVC 패턴:
Model: 도메인 객체 및 DTO를 통해 비즈니스 데이터를 표현
View: 사용자에게 정보를 표시하는 역할
Controller: 사용자의 요청을 처리하고 적절한 응답을 반환

Controller(사용자요청받고처리) - service(비즈니스로직처리) - repository(데이터베이스작업) - model(데이터구조정의)
권한 관리: Spring Security를 통해 인증 및 권한 관리 기능 구현
ktison은 인증처리를 SSO 사용
sso:통합로그인(한번의 로그인으로 모든 서비스 접근 장점 )

로깅: Logback 사용 (logback-spring.xml spring 에서 기본으로 읽는다)
로그 아카이빙, 필터링, 조건부 로깅 및 성능 등 장점
인터셉터: 요청 처리 전후에 공통 기능을 구현하여 코드 중복을 줄입니다. (예)세션처리)
추가 기능
JPA: 객체 관계 매핑을 통해 데이터베이스와의 상호작용을 간소화 /JPA및ORM 학습하면 좋음/
CI/CD: Jenkins, Git 등을 활용하여 지속적 통합 및 배포 프로세스 구축 /jenkins한번쯤 설치하면 좋음/ /git학습필요/
서버준비: ktcloud, AWS, Azure 등 클라우드 서비스 활용 /AWS, Azure 학습하면 좋음/
이 부분 수정
3.배포 및 반영
내장 톰캣 사용: java -jar ktis.jar 명령어로 애플리케이션 실행
WAS: 내장 톰캣
Web: Nginx를 통해 정적 파일 서빙 및 리버스 프록시 설정(보안)
server {
    listen 80;  # HTTP 포트
    server_name example.com;  # 도메인 이름

    # 정적 파일 서빙
    location ~* \.(jpg|jpeg|png|gif|ico)$ {
        alias /path/to/static/files/;  # 정적 파일이 위치한 경로
    }

    # Java 애플리케이션 프록시
    location / {
        proxy_pass http://localhost:8080;  # Java 애플리케이션이 실행 중인 주소
        proxy_set_header Host $host;  # 원래의 Host 헤더 전달
        proxy_set_header X-Real-IP $remote_addr;  # 클라이언트의 실제 IP 전달
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  # 포워드된 IP 주소
        proxy_set_header X-Forwarded-Proto $scheme;  # 프로토콜 정보 전달
    }
}
도메인 관리
네임서버에서 도메인 관리 및 IP 주소 확인
사용자가 요청한 도메인에 대한 IP 주소를 네임서버에서 찾아서 연결
https://xn--c79as89aj0e29b77z.xn--3e0b707e/
ktis.co.kr (ncloud에서 네임서버 관리)

예시) ktison-web
1)사용자가 ktison.ktis.co.kr 브라우저 요청 -> 해당 도메인의 네임서버 주소를 찾고 -> 네임서버에서 해당 도메인의 ip를 찾는다. -> 그리고 사용자 브라우저에서 ktison.ktis.co.kr을 해당 ip로 이동
*이때 host를 변경 해서 원하는 도메인으로 변경 테스트 가능

통신 확인
해당 서버에서 - 디비서버
telnet 10.220.68.82 5445(공인)
telnet 10.21.11.10 5445(cip)
https://cloud.kt.com/console/g/networklist
사용자가 -> 해당 서버
@방화벽 보안파트에 요청(itsm작성)
보안성 검토 요청
시스템 오픈 전 보안성 검토 요청 및 관련 내용 처리 완료 후 오픈
관련 부서: ERM
@전자결재에서 '보안성 검토 요청' 관련 문서 확인
