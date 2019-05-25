---
layout: post
title: 19.05.22 studymanager project 진행과정
category: Project
---

# 19.05.22 studymanager project 진행과정
### curriculum details 등록하기
- curriculum details 등록 페이지로 이동할 때 curriculumId를 파라미터로 보낸다.
- curriculumId를 통해 curriculumContent와 해당 studyName정보를 화면에 보여준다.
- curriculum details를 json데이터의 list형태로 만들어 ajax를 통해 보내고 api controller에서 해당 내용을 담은 DTO의 list로 받아 등록한다.

<br>



- details를 list형태로 만들어 보낸다.

```javascript
function curriculumdetaillist() {
        var curriculumDetailContent = $('#curriculumDetailContent').val();
        var curriculumId = $('#curriculumId').val();

        var token = $("meta[name='_csrf']").attr("content");
        var header = $("meta[name='_csrf_header']").attr("content");

        var contentlength = $('input[name="curriculumDetailContent"]').length;

        var arr = new Array();
        $("input[name=curriculumDetailContent]").each(function (index, item) {
            var obj = new Object();
            obj.curriculumId = $('#curriculumId').val();
            obj.curriculumDetailContent = $(item).val();
            arr.push(obj);
        });

        var jsonData = JSON.stringify(arr);

        $.ajax({
            url: "/api/curriculumDetails/add",
            type: 'POST',
            data:jsonData,
            async: true,

            contentType: "application/json",
            beforeSend: function( xhr ) {
                xhr.setRequestHeader(header, token);
            },
            success: function (data) {
                location.href='/study/studyDetail/'+data;
            },
            error: function (err) {
                console.log(err.toString());
            }
        });
    }

```

<br>

- controller에서 DTO형태로 받아 저장한다.

```java

  //커리큘럼 디테일 등록하기
    @PostMapping("/add")
    public ResponseEntity<Long> addCurriculum(@Valid @RequestBody List<CurriculumDetailFormDto> curriculumDetailFormDtoList){
        Long curriculumId = curriculumDetailService.addCurriculumDetail(curriculumDetailFormDtoList);
        Long studyId = studyService.getStudyNameByCurriculumId(curriculumId).getStudyId();
        return new ResponseEntity<>(studyId, HttpStatus.CREATED);
    }


```

