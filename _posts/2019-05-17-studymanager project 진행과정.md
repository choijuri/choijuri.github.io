---
layout: post
title: 19.05.17 studymanager project 진행과정
category: Project
---

# 19.05.17 studymanager project 진행과정
### http 상태코드를 반환 하기
- api controller의 결과로 원하는 http 상태코드를 반환 하도록 수정한다.

<br>



- api controller 에서 http 상태코드를 설정하여 반환하도록 수정

```java
@PostMapping
    public ResponseEntity<SendMessageDto> sendMessage(@Valid @RequestBody SendMessageDto sendMessageDto){
        messageService.addMessage(sendMessageDto);
        return new ResponseEntity<>(sendMessageDto, HttpStatus.CREATED);
    }

```
<br>

