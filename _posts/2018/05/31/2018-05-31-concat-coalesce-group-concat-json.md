---

title: CONCAT,COALESCE,GROUP_CONCAT을 이용해서 json처럼 뽑아버리기
layout: post 
category: devops 
tags: 
  - mysql
  - query
---

# CONCAT,COALESCE,GROUP_CONCAT을 이용해서 json처럼 뽑아버리기

```
SELECT

  OL.ORDER_MENU_ID AS ORDER_MENU_ID
  ,OL.ORDER_ID AS ORDER_ID
  ,OL.MENU_GROUP_ID AS MENU_GROUP_ID
  ,OL.MENU_ID AS MENU_ID
  ,OL.MENU_NM AS MENU_NM
  ,OL.SELLING_PRICE AS SELLING_PRICE
  ,SUM(OL.TOTAL_SELLING_PRICE) AS TOTAL_SELLING_PRICE
  ,OL.DESCRIPTION AS DESCRIPTION
  ,PL.ORDER_MENU_ID AS OP_ORDER_MENU_ID
  ,PL.OPT_NAME AS OP_OPT_NAME
  ,PL.MUST_YN AS OP_MUST_YN
  ,PL.COUNT_YN AS OP_COUNT_YN
  ,PL.COUNT AS OP_COUNT
  ,PL.TYPE AS OP_TYPE
  ,PL.OPTION_PRICE AS OP_OPTION_PRICE
  ,CONCAT(
      '[',
      COALESCE(
          GROUP_CONCAT(
              CONCAT(
                  '{',
                  '\"order_menu_id\": \"', OL.ORDER_MENU_ID, '\", ',
                  '\"menu_nm\": \"', OL.MENU_NM, '\"',
                  '}')
              ORDER BY menu_nm ASC
              SEPARATOR ','),
          ''),
      ']') AS orderOptionList
FROM
  ORDER_MENU_LIST OL
  LEFT JOIN ORDER_MENU_OPTION_LIST PL
    ON OL.ORDER_MENU_ID = PL.ORDER_MENU_ID

WHERE OL.ORDER_ID = 'ORD_FQV_20180531075106'
GROUP BY MENU_ID
ORDER BY MENU_ID DESC;
```

![1](/assets/imgs/2018/05/31/2018-05-31.png)