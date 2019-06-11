---
layout: post
title: 프로그래머스) JadenCase 문자열 만들기

category: Algorithm
---

### 프로그래머스) JadenCase 문자열 만들기
https://programmers.co.kr/learn/courses/30/lessons/12951

### 문제
-  JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

제한 조건
s는 길이 1 이상인 문자열입니다.
s는 알파벳과 공백문자(" ")로 이루어져 있습니다.
첫 문자가 영문이 아닐때에는 이어지는 영문은 소문자로 씁니다. 

<br><br>

- 시행착오 : 처음 모든 문자를 소문자로 바꾸고 공백을 기준으로 split()메소드를 사용하여 잘라 배열에 넣었다. 각각 배열의 0번째 인덱스의 값을 대문자로 바꾸는 방법을 사용했는데 공백문자가 여러개가 겹쳐져 있을경우 테스트를 통과하지 못했다. 

<br>

- 방법 :  문자열의 길이만큼 반복문을 돌면서 공백을 확인하고 공백이라면 boolean값으로 true를 넣어 대문자로 바꾼 후 boolean값을 false로 바꾼다. 확인하여 false인 값을 가지면 소문자로 바꾸도록 하였다.

<br>


```java

class Solution {
  public String solution(String s) {
      StringBuffer answer = new StringBuffer();
        boolean f = true;
        for(int i=0; i<s.length(); i++){
            if(s.charAt(i) == ' '){
                answer.append(s.charAt(i));
                f = true;
            }else {
                if(f == true) {
                    answer.append(Character.toUpperCase(s.charAt(i)));
                    f = false;
                }else {
                    answer.append(Character.toLowerCase(s.charAt(i)));
                }
            }
        }
    return answer.toString();
  }
}

```

<br>
