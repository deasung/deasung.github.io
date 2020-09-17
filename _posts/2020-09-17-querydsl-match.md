---
title: springboot querydsl jpa match 방언추가해서 사용하는법
tags: [spring, jpa, querydsl]
categories: [spring, jpa, querydsl]
published: true
comments : true
---

요구사항중에 FullText 검색이 필요한 이슈가 생겨서 삽질한 기록 🤔

쿼리로 하면 간단하지만 기존 로직이 querydsl을 이용해서 한 로직이라 최대한 기존 로직에 맞춰서 수정해야하는 상황 😇

# 1. application.yml 설정 변경 
```
jpa:
    properties:
      hibernate:
        dialect: app.config.MySQLDialectCustom 
        
```


# 2.application.yml→jpa dialect에 적용할 방언클래스 생성

```
package app.config;

import org.hibernate.dialect.MySQL57Dialect;
import org.hibernate.dialect.function.SQLFunctionTemplate;
import org.hibernate.dialect.function.StandardSQLFunction;
import org.hibernate.type.StandardBasicTypes;

public class MySQLDialectCustom extends MySQL57Dialect {

  public MySQLDialectCustom() {
    registerFunction(
        "group_concat",
        new StandardSQLFunction("group_concat", StandardBasicTypes.STRING)
    );

    registerFunction(
        "timestampadd",
        new StandardSQLFunction("timestampadd", StandardBasicTypes.DATE)
    );

    registerFunction(
        "match",
        new SQLFunctionTemplate(StandardBasicTypes.DOUBLE, "match(?1) against (?2 in boolean mode)")
    );

  }
}
```
- 디비엔진에 맞게 디비방언 클래스를 상속 MySQL57Dialect
- 사용자 정의함수 match 추가
    ```
    registerFunction(
            "match",
            new SQLFunctionTemplate(StandardBasicTypes.DOUBLE, "match(?1) against (?2 in boolean mode)")
        );
    ```


# 3.querydsl 사용하는법

```
BooleanBuilder builder = new BooleanBuilder();

      

String words = reviewFilterDTO.getSearchWords().stream()
	.filter(word -> word != null && !word.trim().isEmpty())
  .findFirst().get();


if (StringUtils.isNotEmpty(words)) {

  //AND MATCH (qtest.text) AGAINST ('test*' IN boolean mode)
	NumberTemplate booleanTemplate = Expressions.numberTemplate(Double.class, "function('match',{0},{1})", qTest.text, "+" + words + "*");

  builder.and(booleanTemplate.gt(0));

  jpaQuery.where(builder);

}
```

잘 동작함 😀