---
layout: post
title: 19.04.26 studymanager project 진행과정
category: Project
---

# 19.04.26 studymanager project 진행과정
### recruitstudyRegister 페이지 등록 & 다른 사용자에게 message를 보내는 기능 추가
- recruitstudy의 상세페이지에서 메시지를 보내는 모달을 띄운다.
- 모달안에서 입력받은 내용을 모집스터디 관리자에게 메시지를 보낸다.
- RestAPI를 사용하여 message를 보낸다.


```javascript
    <script type="text/javascript">

        function sendmessage() {
            var receiver = document.getElementById("receiver").value;
            var sender = document.getElementById("sender").value;
            var messageContent = document.getElementById("messageContent").value;
            alert(receiver +' , '+sender+' , '+ messageContent );

            var token = $("meta[name='_csrf']").attr("content");
            var header = $("meta[name='_csrf_header']").attr("content");

            var JSONObject = {'receiver': receiver, 'sender' : sender, 'messageContent' : messageContent};
            var jsonData = JSON.stringify(JSONObject);

            $.ajax({
                url: '/api/message',
                method: 'post',
                data: jsonData,
                async: false,
                contentType: "application/json",

                success: function (data) {
                    toggleModal();
                    alert('성공!');
                },
                beforeSend: function( xhr ) {
                    xhr.setRequestHeader(header, token);
                },
                error: function (err) {
                    console.log(err.toString());
                }
            });


        }
    </script>

```
