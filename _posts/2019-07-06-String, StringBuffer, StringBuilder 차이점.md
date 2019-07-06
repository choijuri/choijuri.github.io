---
layout: post
title: String, StringBuffer, StringBuilder의 차이점
category: JAVA
---

## String, StringBuffer, StringBuilder의 차이점

`모두 문자열을 저장하거나 관리하는 클래스` 

> String     

String은 new 연산자를 통해 생성되면 그 인스턴스 메모리 공간이 절대 변하지 않는 **불변클래스**입니다. 그래서 문자열에 더하거나 빼는 등 변화를 주더라도 메모리 공간이 변하는 것이 아니라 새로운 String 객체를 new로 생성하며 새로운 메모리 공간을 만들게 됩니다. 기존의 문자열은 GC에 의해 제거되어야 하고 문자열의 연산이 많아 지면 새로운 객체를 만드는 오버헤드가 발생하여 성능이 떨어질 수 있는 단점이 있습니다.

<br>

> StringBuffer와 StringBuilder

StringBuffer와 StringBuilder는 가변클래스로 한번 생성한 후에 연산이 필요한 경우 크기를 변경시켜 문자열 연산을 수행합니다. 따라서 문자열 연산이 자주 있을때 사용한다면 성능이 좋습니다.

StringBuffer는 Thread-safe하기 떄문에 멀티쓰레드 환경에서 synchtonized키워드가 지원되어 동기화가 가능합니다.
하지만 StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서 적합하지 않습니다.

<br>
<hr>
<br>

+JDK1.5버전 이상부터는 String으로 연산을 하면 StringBuilder로 컴파일 하도록 동작하지만 String객체를 생성하는 것은 동일하므로 연산을 많이 사용한다면 StringBuilder, 동기화가 필요한 멀티 쓰레드 환경이라면 StingBuffer를 사용하는 것이 유리합니다.

<br>

`참고`   
https://jeong-pro.tistory.com/85 