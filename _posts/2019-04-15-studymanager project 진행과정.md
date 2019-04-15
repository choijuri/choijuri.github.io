---
layout: project
title: 19.04.15 studymanager project 진행과정
---

# 19.04.15 studymanager project 진행과정
### index.html만들기
- 모바일 화면으로 상세메뉴는 버튼을 누르면 오른쪽에서 나오도록 만든다.
    - input type="checkbox"로 하며 check가 되면 메뉴가 나온다. 
- 컨텐츠는 각각 db에 있는 것으로 불러와야 하기 때문에 임의로 만들어서 형태만 생성함.

####     문제점
- css의 checked를 사용하여 적용하였지만 메뉴가 움직이지 않음
    - 같은 블록안에 싸여 있어야 했는데 다른 블록에 input과 label / menu 가 분리되어 있었다.
    - 같은 블록안에 넣어 수정한 후에 잘 적용되었다.
    -checked속성으로 display: none / block 을 사용하려면 같은 블록안에 넣어준다.



