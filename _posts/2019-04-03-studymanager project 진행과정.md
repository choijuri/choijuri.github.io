---
layout: post
title: 19.04.03 studymanager project 진행과정
category: Project
---

# 19.04.03 studymanager project 진행과정
### 회원가입 시 입력된 정보 확인하기
- 회원가입 시 가입된 정보의 유효성을 검사한다.
    - java script로 형식을 확인한 후 메시지를 띄운다.
    - 모든 정보 입력후 가입 버튼을 눌렀을때 입력한 모든 정보에 대해 확인 후 controller로 이동한다.

    -각 항목의 정규식
    ```
    var regEmail = /([\w-\.]+)@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.)|(([\w-]+\.)+))([a-zA-Z]{2,4}|[0-9]{1,3})(\]?)$/;

     var regPasswd = /^[0-9a-z]{8,12}$/;

     var regPhone = /^[0-9]{11,11}$/;
    ```

    -비밀번호와 비밀번호 확인
    ```
    function tocheckPw2() {
            var regExpId = /^[0-9a-z]{8,12}$/;
            var userPWD = document.getElementById("userPWD").value;
            if (!regExpId.test(userPWD)) {
                document.getElementById('check2').innerHTML = '비밀번호는 숫자, 영문, 특수문자 조합으로 8~12자리를 사용해야 합니다.';
                return false;
            } else {
                document.getElementById('check2').innerHTML = '';
                return true;
            }

        }
    ```

    -각 항목에 대한 확인
    마지막으로 가입버튼을 눌렀을 때 모든 항목을 확인해준다.<br>
    각 항목에 통과하지 못한다면 false가 return되므로 alert창을 띄워준다.
    ```
    if (!r1 && !r2 && !r3 && !r4) {
                alert("다시 입력해주세요.");
                return false;
            }
    ```



    <br>
    
- - -

    
####     과정 

- 중복확인 버튼을 눌렀을 때 확인되는 것은 다른 email을 사용하려는 과정에서 불편함을 발견해 수정했다.
- focusout되는 순간 다른 항목을 입력하려고 넘어간 것이므로 그 항목에 대해서 focusout되면 바로 확인 하고 형식에 맞지 않는다면 빨간색으로 메시지를 띄운다.
- 메시지를 무시하고 가입버튼을 눌렀을 경우를 생각하여 마지막으로 확인을 한다.
- 프론트를 무시하고 넘어온 경우를 생각하여 각 항목에 맞춰 validation 설정을 했다.