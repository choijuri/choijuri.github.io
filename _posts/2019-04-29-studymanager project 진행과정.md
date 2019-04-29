---
layout: project
title: 19.04.29 studymanager project 진행과정
---

# 19.04.29 studymanager project 진행과정
### 사용자가 받은 message의 readCount칼럼 추가 및 기능 구현
 - 테이블 추가, 기능 구현

<br>

 -mysql 에 칼럼추가
```
ALTER TABLE message add read_count INT UNSIGNED NOT NULL DEFAULT 0;
```

-MessageRepository에 readCount+1하는 메소드 추가
```java
@Modifying
@Query("UPDATE Message m SET m.readCount = m.readCount+1 WHERE m.messageId =:messageId")
public void modifyReadCount(@Param("messageId") Long messageId);
```

