---
layout: post
title: 19.04.22 studymanager project 진행과정
category: Project
---

# 19.04.22 studymanager project 진행과정
### curriculumregister 화면 만들기
- curriculum등록하는 페이지를 만든다
    - curriculum은 사용자에 따라서 개수가 다르다.
    - +버튼을 누를때마다 입력할 수 있는 폼이 추가되고, 마지막 input박스에만 -버튼이 생긴다.
    - input박스는 10개까지만 생성 가능하다.
    - 각각 input 박스는 모두 같은 name을 가지고 그 값을 배열로 넘겨받는다.



-버튼을 누를때 생성될 input박스
```javascript
$(document).ready(function () {
            var num = 1;
            $('#plusbutton').click(function () {
                num++;
                if (num < 11) {
                    $('.aa').append(
                        '<div class="aaa" style="overflow: hidden;">' +
                        '<label class="curriculum" for="curriculumContent" style="font-size: 1.3em; display: block; text-align: left; margin-top:3%;"  >' + 'STEP ' + num + ' :' + '</label>' +
                        '<input type="text" id="curriculumContent" name="curriculumContent[]" style="padding:2% 1%;margin: 1% auto;width:85%; float: left;"\n' +
                        '                   placeholder="커리큘럼을 입력해주세요" autofocus required> ' +
                        '</div>'
                    )} else {
                    alert('더이상 추가할 수 없습니다!');
                }
                $('div[class=aaa]:last').append('<img id="minus" src="/images/211774-64.png" style="margin-top:3%; width:10%; float:right;  ">')
               if(num>1){
                $('#minus').not('div[class=aaa]:last').remove();}
            });
            $(document).on("click", "img[id=minus]:last", function () {
                $('div[class=aaa]:last').remove();
                $('#minus').not('div[class=aaa]:last').remove();
                $('div[class=aaa]:last').append('<img id="minus" src="/images/211774-64.png" style="margin-top:3%; width:10%; float:right; ">')
                num--;
            });
        });

```


#### 해결
- -버튼을 마지막 input에 주는 것에서 시간을 많이 할애하였다.
- 마지막 input에 버튼을 추가로 생성하고, 마지막이 아닌 곳에 버튼을 없애는 방법으로 해결하였다.
<br><br>

####     문제점
- api를 생성하여 입력된 curriculum들을 배열로 넘겨야 하는 부분

