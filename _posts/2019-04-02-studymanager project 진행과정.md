---
layout: post
title: 19.04.02 studymanager project 진행과정
category: Project	
---

# 19.04.02 studymanager project 진행과정
### 회원가입 시 email 중복확인 API 설정
- 이메일을 입력한 후 중복확인 버튼을 누르면 중복된 값이 있는지 확인한다.
    - jquery의 ajax를 이용하여 POST 방식으로 json형식의 값을 넘긴다.

    - Controller에서 RequestBody로 Map<>형식의 값을 받아 받아온 email로 중복된 값의 존재유무를 확인한다.
        - count의 int값을 받아와 중복된 값이 있으면 1, 없으면 0을 반환한다.
    
    - 중복된 email의 값이 없다면 disabled 설정을 추가하여 값의 제한을 걸어준다
        - 회원가입을 진행할 때 중복확인을 통과하였는지 여부를 확인하기 위해서 추가한다.



    ```
    <script>
        $(document).ready(function () {
            $("#check-email").unbind("click").click(function (e) {
                e.preventDefault();
                fn_emailCheck();

            });
        });

        function fn_emailCheck() {
            var email =$('#email').val();
            var userData = {'email' : email}
            var jsonData = JSON.stringify( userData );

            if(email<1){
                document.getElementById('checkemail').innerHTML = 'email을 입력해주세요!';
            }else {
                $.ajax({
                    type : 'post',
                    url : '/api/emailCheck',
                    data : jsonData,
                    contentType: "application/json",
                    error : function (err) {
                        console.log(err.toString());
                        alert("서버가 응답하지 않습니다. \n 다시 시도해주시기 바랍니다.");

                    },
                    success : function (data) {
                        if(data==0){
                            $('#email').attr('disabled', true);
                            document.getElementById('checkemail').innerHTML = '사용가능한 email 입니다!';
                        }else if(data==1){
                            document.getElementById('checkemail').innerHTML = '이미 존재하는 email 입니다. 다른 email을 사용해주세요!';
                        }else{
                            alert("에러가 발생했습니다!");
                        }
                    }
                });
            }
        }


    </script>
    ``` 
    <br>
    
- - -

    
#### 해결한 문제점

- json형식의 데이터를 변환하여 Controller로 보내면 Map<>형식으로 변환된다. 이 과정에 대한 처리가 부족하여 이미 있는 email에 대해서도 사용가능한 email이라는 메시지가 출력되었다. 
- Map의 key값인 email로 value값안 받아온 email을 꺼내 확인해 문제를 해결하였다.