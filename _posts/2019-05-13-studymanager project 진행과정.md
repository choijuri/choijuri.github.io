---
layout: post
title: 19.05.13 studymanager project 진행과정
category: Project
---

# 19.05.13 studymanager project 진행과정
### recruitstudyApiController 수정
- recruitStudy를 등록할 떄 사용할 ApiController를 수정한다.
- Controller로 이용했지만 Api를 사용하여 페이지 이동없이 등록을 하며, 성공과 실패에 따른 http status code를 반환하도록 구현.

<br>

-ajax를 이용하여 데이터를 json데이터로 변환하여 보낸다.
```javascript
     $('#next').click(function () {
                var token = $("meta[name='_csrf']").attr("content");
                var header = $("meta[name='_csrf_header']").attr("content");

                var recruitName = document.getElementById("recruitName").value;
                var recruitNumberV = document.getElementById("recruitNumber").value;
                var recruitNumber= Number(recruitNumberV);

                var recruitContent = document.getElementById("recruitContent").value;

                var sido1 = document.getElementById("sido1").value;
                var gugun1 = document.getElementById("gugun1").value;
               
                var categorysel = document.getElementById("categoryId");
                var categoryId = Number(categorysel.options[categorysel.selectedIndex].value);


                var JSONObject = {'recruitName': recruitName, 'sido1' : sido1, 'gugun1' : gugun1,
                    'recruitNumber' : recruitNumber, 'recruitContent' : recruitContent,
                    'categoryId' : categoryId};
                var jsonData = JSON.stringify(JSONObject);
                alert(jsonData);

                $.ajax({
                    url: '/api/recruitstudies',
                    method: 'post',
                    data: jsonData,
                    async: false,
                    contentType: "application/json",
                    beforeSend: function( xhr ) {
                        xhr.setRequestHeader(header, token);
                    },
                    success: function (data) {
                        alert(data);
                        location.href='/recruitstudy/list';
                    },
                    error: function (err) {
                        alert(err.toString());
                    }
                });
            })

        });
```

<br>



    

#### 문제해결
- selectbox에서 선택된 값을 가져오기 위한 코드를 사용했다. 이 과정에서 아무 값도 가져오지 못하는 에러가 발생하였다. 해당 selectbox는 jqeury를 사용하여 안의 구성요소인 option의 내용이 바뀌는 형태로 만들어져 있다. 
- option의 요소가 해당값의 value값을 가지는 형태로 수정한 코드로 선택된 값을 지정해 주지 않아도 해당 id의 value 값을 가져왔다. 

```javascript
  var sidosel = document.getElementById("sido1").value;
  var sido1 = sidosel.options[sidosel.selectedIndex].value;
```

- 수정 후

```javascript
    var sido1 = document.getElementById("sido1").value;
```