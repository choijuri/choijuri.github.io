---
layout: post
title: 19.05.12 studymanager project 진행과정
category: Project
---

# 19.05.12 studymanager project 진행과정
### recruitstudyApiController 작성, 스터디 등록 api수정
- studyApiController를 작성하여 study등록과정을 apiController로 작동시키고 return type으로 http status code를 반환하도록 구현한다.
- 위의 방법과 마찬가지로 recruitStudyApiController를 작성한다.
<br>

-StudyApiController코드 
```java
    //스터디 등록하기, 스터디유저 추가
    @PostMapping
    public ResponseEntity<Long> addStudy(@Valid @RequestBody StudyFormDto studyFormDto, BindingResult bindingResult){
        System.out.println(studyFormDto.getCategoryId());

        if(bindingResult.hasErrors()){
            throw new IllegalArgumentException(bindingResult.toString());
        }
        Long studyId = studyService.addStudy(studyFormDto);
        StudyManagerSecurityUser securityUser = (StudyManagerSecurityUser) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
        studyUserService.addStudyUser(studyId,securityUser.getId());
        return new ResponseEntity<>(studyId, HttpStatus.CREATED);
    }
```

<br>



 
