## 각종 툴 혹은 꿀팁 모음


# DBEAVER
https://3rdscholar.tistory.com/83
# git
https://learngitbranching.js.org/?locale=ko
# springboot에서 application.yml이란? 환경설정을 뜻함
예시)
spring.profiles: dev

spring:
  datasource:
    platform: postgresql
    url: jdbc:postgresql://ip/db이름 #개발서버
    username: 
    password: 
    driverClassName: org.postgresql.Driver
    
file.upload.path: 경로

server:
  port: 8081
  servlet:
    session:
      cookie:
        secure: true
        http-only: true
        
logging.path: 경로

Run Configurations에서 -Dspring.profiles.active=dev 이런식으로 설정하면 위에 설정한거로 붙음

# 프로젝트 어디에 있는건지 찾으려고 할때 -> 인텔리제이 ctrl+shift+f도 있지만, 웹에 접속해서 f12번 누르고 마우스로 클릭해서 경로 찾는 방법도 있다.
  웹에서 돌아가는거 하나씩 까보려면 동작했을때 인텔리제이에 나오는 로그를 보면 된다

# 인텔리제이 실행 창 : View -> Tool Windows -> Run
# Git log 창 : git->show git log
#TCP DUMP TCP 로그 보는법 :
https://discourse.ubuntu-kr.org/t/tcpdump-flags-s/23600

# Gradle 표준 레이아웃 (기본 구조)
Gradle을 사용하는 프로젝트에서도 Maven과 유사하게 'src/main/resources' 디렉터리가 주로 사용됩니다. 
gradle-project-root
|-- src
|   |-- main
|   |   |-- java          // Java 소스 코드
|   |   |-- resources     // 웹 애플리케이션 관련 리소스 파일 (프로퍼티 파일, XML 파일 등, HTML, CSS, JavaScript 등)
|   |-- test
|       |-- java          // 테스트용 Java 소스 코드
|       |-- resources     // 테스트 리소스 파일
|-- build                 // 빌드 결과물이 생성되는 디렉토리
|-- build.gradle          // Gradle 프로젝트 설정 파일


# Spring boot Process finished with exit code 0 해결
https://blockchain-baam.tistory.com/58
 
