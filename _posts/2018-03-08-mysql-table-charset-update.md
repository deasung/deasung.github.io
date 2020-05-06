---

title: Mysql Table charset 변경 / AUTO_INCREMENT = 1로 초기화
published: true
---



```
ALTER TABLE 테이블명 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

```

```
AUTO_INCREMENT = 1로 초기화

예) test_table의 자동증가를 1부터 시작하게 최기화 
ALTER TABLE 테이블명 AUTO_INCREMENT=1
```
