## 동적 웹 프로젝트 (Dynamic Web Project)

### JSP 개발 환경 도구

자바 개발환경: JDK ( http://www.oracle.com/kr/java )

웹서버: tomcat ( Http://tomcat.apache.org )

통합 개발 환경: eclipse

### 동적 웹 프로젝트 구조

![image](https://user-images.githubusercontent.com/16650632/150706118-01acae0d-d109-4e15-b124-d25b0971462b.png)

*표준 웹 애플리케이션 배치 디스크립터(web.xml)

### 톰캣 서버 에러 해결: Port 8080 already in use

#### 1. 톰캣 이용 port 변경

#### 2. port 사용중인 프로그램 종료

    * windows (CMD 관리자 모드)

    netstat -aon | find "8080"

    taskkill /F /PID {process id}

    * mac (terminal)

    lsof -i :8080

    kill {process id}

### 스크립트 태그

JSP 페이지가 서블릿 프로그램에서 서블릿 클래스로 변환할 때 JSP 컨테이너가 자바 코드가 삽입되어 있는 스크립트 태그를 처리하고 나머지는
HTML 코드나 일반 텍스트로 간주

선언문(declaration) <%! ... %> : 자바 (전역) 변수, 메소드 정의

스크립틀릿(scriptlet) <% ... %> : 자바 로직 코드 작성, 서블릿 프로그램으로 변환될 때 \_jspService() 메소드 내부에 배치된다.

표현문(expression) <%= ... %> : 변수, 계산식, 메소드 호출 결과를 문자열 형태로 출력

### 디렉티브 태그

<%\@ page ... %> : JSP 페이지에 대한 정보 설정

    <%\@ page import = "java.util.Date" %>

    <%\@ page session = "true" %> : JSP 페이지의 HTTP 세션 사용 여부를 설정 (session 내장 객체 사용 설정)
    
    <%\@ page buffer = "none/32kb/..." %> : 출력 버퍼 크기 설정
    
    <%\@ page errorPage = "ErrorPage.jsp" %> : 이동할 오류 페이지 설정  
    
    <%\@ page isErrorPage = "true" %> : 현재 페이지를 오류 페이지로 설정

<%\@ include ... %> : JSP 페이지의 특정 영역에 다른 문서를 포함

    <%\@ include file="파일명" %>

<%\@ taglib ... %> : JSP 페이지에서 사용할 표현 언어, JSTL, 사용자 정의 태그 등 태그 라이브러리 설정

    <%\@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
    
    <c:forEach var="k" begin="1" end="10" step="1">
      <c:out value="${k}" />
    </c:forEach>      

### 액션 태그

서버나 클라이언트에게 어떤 행동을 하도록 명령하는 태그로 페이지와 페이지 사이를 제어하는 : <jsp: ... />

<jsp:forward page="파일명" /> : JSP 컨테이너는 forward 액션 태그를 만나면 출력 버퍼에 저장되어 있던 내용을 모두 삭제

<jsp:include page="파일명" flush="false" /> : flush="false" -> 외부파일로 제어 이동시 출력 버퍼에 저장한 결과를 처리

<jsp:param ... /> : forward, include, plugin 태그에 인자를 추가

    <jsp:forward page="파일명">
       <jsp:param name="매개변수명" value="값" />
    </jsp:forward>

#### 자바빈즈 액션 태그

![image](https://user-images.githubusercontent.com/16650632/151093002-cc390214-b4f1-4716-a336-6d1f02ddb49e.png)

화면을 표현하는 JSP 페이지와 로직을 구현하는 역할을 하는 자바빈즈(자바 클래스)를 분리

자바빈즈 작성 규칙: 자바 클래스는 java.io.Serializable 인터페이스를 구현, 기본 생성자, private 멤버 변수, getter/setter() 메소드

* 자바 직렬화 : 자바 시스템 내부에서 사용되는 객체/데이터를 외부의 자바 시스템에서 사용할 수 있도록 바이트 형태로 데이터 변환하는 기술

<jsp:useBean id="" class="" scope="" /> : JSP에서 자바빈즈를 사용하기 위해 자바 클래스를 선언하고 초기화하는 태그 (scope: page, request, session, application)

    MemberBean member = (MemberBean) request.getAttribute("member");
    
<jsp:setProperty name="자바빈즈 식별이름" property="프로퍼티 이름" value="값" /> : 자바빈즈의 setter() 메소드에 접근하여 프로퍼티 값을 저장

<jsp:getProperty name="자바빈즈 식별이름" property="프로퍼티 이름" />















