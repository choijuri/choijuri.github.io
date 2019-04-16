---
layout: project
title: 19.04.16 studymanager project 진행과정
---

# 19.04.16 studymanager project 진행과정
### study main.html thymleaf로 수정/ user 이름 띄우기
- thymleaf 형식을 추가한다.
 - get방식으로 main.html 로 보내는 controller에서 login여부를 같이 model에 담아서 보낸다.
 - main 에서 로그인된 user의 이름을 띄우도록 thymleaf 문법에 맞춰 작성한다.

controller
 ```java
  model.addAttribute("isLogin",(!SecurityContextHolder.getContext().getAuthentication().getPrincipal().equals("anonymousUser"))? true : false);
        
```

main.html
 ```html
 <li class="fir" th:if="${isLogin}" >
	<h3  th:text="${#authentication.principal.name}+'님 환영합니다'">님 환영합니다</h3>
	<a href="/users/mypage">MY</a> / <a href="/logout">LOGOUT</a>
 </li>
 ```

 ####     과정
 - get방식으로 보내진 main.html에서 thymleaf를 사용하기 때문에 th:if로 로그인이 되어있는지 확인한다.
 - login이 되어있지 않으면 접근할 수 없는 페이지이기 떄문에 로그인이 되지 않은상태는 만들지 않았다. 만약 접근 가능하다면 로그인 버튼을 만들어 주면 될 것 같다.