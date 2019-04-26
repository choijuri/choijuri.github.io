---
layout: project
title: 19.04.24 studymanager project 진행과정
---

# 19.04.24 studymanager project 진행과정
### curriculum 등록하기
- 커리큘럼을 등록할 때 + 버튼을 누르면 input 창이 추가된다.
- 이 과정에서 입력된 커리큘럼의 양이 사용자마다 달라 받아온 값을 list형태로 만들어서 넘겨야 한다.
- json 데이터로 변환하여 api를 통해 등록한다.

<br>
-입력된 값을 list로 만들어 json data로 변환

```javascript
            var arr = new Array();
            $("input[name=curriculumContent]").each(function (index, item) {
                var obj = new Object();
                obj.studyId = $('#studyId').val();
                obj.curriculumContent = $(item).val();
                arr.push(obj);
            });

            var jsonData = JSON.stringify(arr);
```

<br>
- RestController에서 dto list로 받음

```java
@PostMapping
    public List<CurriculumFormDto> addCurriculum(@Valid @RequestBody List<CurriculumFormDto> curriculumFormDtoList){
        curriculumService.addCurriculum(curriculumFormDtoList);
        return curriculumFormDtoList;
    }
```




####     문제해결
- 페이지에서 넘기기 전에 list형태의 json데이터로 변환하는 과정과 받아온 list형태의 값을 처리하는 과정이 잘 안풀렸지만 찾아본 결과 만들어 놓을 CurriculumDto를 List형태로 받아서 처리하면 잘 동작한다.

