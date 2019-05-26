---
layout: post
title: 19.05.23 studymanager project 진행과정
category: Project
---

# 19.05.23 studymanager project 진행과정
### study list, recruit study list style 수정하기
- list 화면을 보여줄 때 카테고리ID에 따라 색상이 변경되게 설정
- 카테고리 ID에 switch~case문을 이용한다.
- case에 따라 전체 박스에 들어간 속성을 변경해야 하기 때문에 Jqeury를 이용해 부모의 css속성을 변경하도록 한다.

<br>



- switch~case문을 이용

```html
<div th:switch="${study.category.categoryId}" class="study_box" style="width:15%; float: left;">
    <p th:case="1"  class="cate_text" id="text_1" th:text="${study.category.categoryName}">recruitContent</p>
    <p th:case="2"  class="cate_text" id="text_2" th:text="${study.category.categoryName}">recruitContent</p>
    <p th:case="3"  class="cate_text" id="text_3" th:text="${study.category.categoryName}">recruitContent</p>
    <p th:case="4"  class="cate_text" id="text_4" th:text="${study.category.categoryName}">recruitContent</p>
</div>


```

<br>

- 부모를 지칭하는 셀렉터를 이용하여 css 속성값을 변경한다.

```javascript

  $('document').ready(function () {
        $('p#text_1').parent('.study_box').parent('.box').css('border-left', '5px solid #ffcd00');
        $('p#text_2').parent('.study_box').parent('.box').css('border-left', '5px solid green');
        $('p#text_3').parent('.study_box').parent('.box').css('border-left', '5px solid rebeccapurple');
        $('p#text_4').parent('.study_box').parent('.box').css('border-left', '5px solid darkblue');

    });


```

