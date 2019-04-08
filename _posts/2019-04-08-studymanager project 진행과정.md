---
layout: project
title: 19.04.08 studymanager project 진행과정
---

# 19.04.08 studymanager project 진행과정
### csrf 보안 - spring jpa security 사용
- api controller에게 post방식으로 요청할 때 csrf(현재 인증 된 웹 응용 프로그램에서 원치 않는 작업을 실행하도록하는 공격)공격에 방지하여 csrf토큰을 생성하여 hidden tag로 숨겨서 보낸다.

-form이 있는 header 안에 token 설정한다.
```html
 <meta name="_csrf_param" th:content="${_csrf.parameterName}"/>
    <meta name="_csrf" th:content="${_csrf.token}"/>
    <!-- default header name is X-CSRF-TOKEN -->
    <meta name="_csrf_header" th:content="${_csrf.headerName}"/>

```

-해당 form이 보내질 때 header에 hidden tag로 생성된 token을 보내준다.
```javascript
        var token = $("meta[name='_csrf']").attr("content");
        var header = $("meta[name='_csrf_header']").attr("content");

        $.ajax({
                        type: 'post',
                        url: '/api/emailCheck',
                        // data: 'email='+ encodeURIComponent(email),
                        data: jsonData,
                        // datatype: "text",
                        async: false,
                        contentType: "application/json",
                        error: function (err) {
                            console.log(err.toString());
                            alert("서버가 응답하지 않습니다. \n 다시 시도해주시기 바랍니다.");
                            return false;
                        },
                        beforeSend: function( xhr ) {
                            xhr.setRequestHeader(header, token);
                        },
                        success: function (data) {
                            if (data == 0) {
                                $('#checkemail').css('color', 'green');
                                document.getElementById('checkemail').innerHTML = '사용가능한 email 입니다!';
                                return true;
                            } else if (data == 1) {
                                $('#checkemail').css('color', 'red');
                                document.getElementById('checkemail').innerHTML = '이미 존재하는 email 입니다. 다른 email을 사용해주세요!';
                                return false;
                            } else {
                                alert("에러가 발생했습니다!");
                                return false;
                            }
                        }
                        
                    });
```

####     문제해결
-토큰을 생성할 때 thymeleaf에서 사용했기 때문에 th: 을 붙여 형식을 지켜줘야 한다.
