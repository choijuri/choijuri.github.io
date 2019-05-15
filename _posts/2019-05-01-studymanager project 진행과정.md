---
layout: post
title: 19.05.01 studymanager project 진행과정
category: Project
---

# 19.05.01 studymanager project 진행과정
### message 알림 띄우기
- 읽지 않은 message를 조회하여 데이터를 가져온다.
- api controller를 사용하여 페이지가 바뀔떄마다 조회를 하고, 만약 읽지 않은 메시지가 있다면 알림을 띄운다.
- 페이지 이동에 따라 조회하고 추후에 web socket을 사용하여 수정할 계획이다. 

<br>

-GET방식
```javascript
 <script type="text/javascript">
        $(document).ready(function() {
            $.ajax({
                url: '/api/message',
                method: 'get',
                async: true,
                contentType: "application/json",
                success: function (count) {
                    if(count != 0){
                        $('#messageimg').append(
                            '<img src="/images/885612-64.png" style="width:10%;" />'
                        );
                    }
                },
                error: function (err) {
                    console.log(err.toString());
                }
            });
        })
    </script>
```
<br>

-controller에서 읽지않은 message count를 조회
```java
    @GetMapping
    public int getApiMessageCount(){
        StudyManagerSecurityUser securityUser = (StudyManagerSecurityUser) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
        return messageService.getNewMessageCount(securityUser.getId());
    }
```

<br>

####     문제해결
-처음에 user table에 message관련 컬럼을 추가하여 변경이 일어날 때 마다 update를 하는 방식으로 진행하였다. 그 과정에서 user 의 정보는 로그인 할 떄 가져온 후 세션에 저장된 정보로 사용되기 떄문에 user가 로그인 된 상태에서 변경되는 message count가 반영되지 않는 문제를 꺠달고 api를 사용하였다. api를 사용한다면 message count정보를 조회하는 것이 더 효율적이라고 생각하여 user teble에 만든 컬럼은 삭제하였다.