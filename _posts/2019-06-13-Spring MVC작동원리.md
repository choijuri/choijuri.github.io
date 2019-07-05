---
layout: post
title: Spring MVC의 작동원리
category: Spring
---


## 스프링 mvc 동작원리

>Dispacher Servlet 은 요청을 처리하기 위한 모든 연결을 담당합니다
<br>

1. Dispacher Servlet은 요청을 받으면 Handler Mapping 에 검색을 요청하여 요청받은 url에 따라 알맞은 컨트롤러를 찾아 처리 컨트롤러를 Dispacher Servlet에 전달합니다.

2. Dispacher Servlet은 Handler Adapter에게 요청을 위임하는데 Hander Adapter는 컨트롤러의 알맞은 메서드를 호출하여 요청을 처리하고 처리결과를 ModelAndView객체로 변환하여 Dispacher Servlet에 리턴합니다.

3. Dispacher Servlet은 ModelAndView객체를 처리하기 위해 View Resolver를 사용하여 뷰이름에 해당하는 View 객체를 찾거나 생성하여 리턴합니다.

4. Dispacher Servlet은 View Resolver가 리턴한 View 객체에게 응답결과 생성을 요청하고 그 View객체는 브라우저에 결과를 출력합니다. 

<br>
<hr>
<br>

` 초보 웹 개발자를 위한 스프링5 프로그래밍 입문 책과 강의들은 내용을 참고하여 작성하였습니다.`
