---
layout: project
title: 19.05.02 studymanager project 진행과정
---

# 19.05.02 studymanager project 진행과정
### recruitStudy category 검색 기능 추가
- 불러온 recruitStudy list의 카테고리 별로 분류하는 기능 추가
- JPQL을 사용하여 생성된 QClass를 활용하여 카테고리 별 검색과 페이징처리, 제목과 내용에 따른 검색기능을 추가한다.

<br>

-repository에서 jpql을 사용하여 데이터를 가져온다.
```java
    @Override
    public List<RecruitStudy> getRecruitStudy(Long categoryId, int start, int limit, String searchKind, String searchStr) {
        QRecruitStudy qRecruitStudy = QRecruitStudy.recruitStudy;
        JPQLQuery<RecruitStudy> jpqlQuery = from(qRecruitStudy).innerJoin(qRecruitStudy.category).fetchJoin().distinct();

        if(categoryId != null){
            jpqlQuery.where(qRecruitStudy.category.categoryId.eq(categoryId));
        }

        searchWhere(searchKind,searchStr,qRecruitStudy,jpqlQuery);

        jpqlQuery.orderBy(qRecruitStudy.recruitId.desc());
        jpqlQuery.offset(start).limit(limit);
        return jpqlQuery.fetch();
    }
```

<br>


-controller 에서 받아온 정보를 조회한 후 madel에 담아 페이지로 보내준다.
```java
    @GetMapping("/list")
    public String recruitStudyList(
            @RequestParam(name = "page",required = false,defaultValue = "1") int page,
            @RequestParam(name = "searchKind", required = false) String searchKind,
            @RequestParam(name = "categoryId", required = false) Long categoryId,
            @RequestParam(name = "searchStr",required = false) String searchStr,
            Model model
    ){
        model.addAttribute("isLogin",(!SecurityContextHolder.getContext().getAuthentication().getPrincipal().equals("anonymousUser"))? true : false);

        List<RecruitStudy> recruitStudyList = recruitStudyService.searchRecruitStudy(page, categoryId, searchKind, searchStr);
        model.addAttribute("recruitStudyList", recruitStudyList);

        model.addAttribute("categories", categoryService.getCategories());
        return "recruitstudy/recruitstudylist";
    }

```
<br>

-카테고리에 categoryId에 따라 링크를 걸어준다.
```html
<nav class="categorymenu">
    <ul>
        <li th:each="category : ${categories}">
            <a th:href="'/recruitstudy/list?categoryId='+${category.categoryId}" th:text="${category.categoryName}" ></a>
        </li>
     </ul>
</nav>
```