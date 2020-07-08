---
title: AWS -> Athena 셋팅
tags: [aws, athena]
categories: [aws]
published: true
comments : true
---

최근에 회사 개발서버에 AWS 로드밸런서에 여러 리스너를 붙여서 사용중에 특정 api만 실제로 로그봐도 elb단에서 
요청이 없는것 같은 느낌적인 느낌이 들어서 삽질을 해봤다.

실제 elb 로그를 봐야 하므로 elb에 로그 활성화를 시켜줘야 한다.

## 1.로드밸런서 속성 편집 
![](/assets/imgs/2020/07/08/1.png)

## 2.권한에서 AmazonAthenaFullAccess? 를 줌 

IAM -> 권한 추가 
![](/assets/imgs/2020/07/08/2.png)

추가 안하면 쿼리 문 실행시 에러가 나옴. 추가가 필요

## 3.Athena 쿼리 에디터로 가서 테이블을 생성해줘야 한다.
공식문서 보고 따라함

```sql


/* 데이터베이스 생성 */ 
create database elb_db;


/* 테이블 생성 */
CREATE EXTERNAL TABLE IF NOT EXISTS elb_glowpick_net_logs (
            type string,
            time string,
            elb string,
            client_ip string,
            client_port int,
            target_ip string,
            target_port int,
            request_processing_time double,
            target_processing_time double,
            response_processing_time double,
            elb_status_code string,
            target_status_code string,
            received_bytes bigint,
            sent_bytes bigint,
            request_verb string,
            request_url string,
            request_proto string,
            user_agent string,
            ssl_cipher string,
            ssl_protocol string,
            target_group_arn string,
            trace_id string,
            domain_name string,
            chosen_cert_arn string,
            matched_rule_priority string,
            request_creation_time string,
            actions_executed string,
            redirect_url string,
            lambda_error_reason string,
            target_port_list string,
            target_status_code_list string,
            new_field string
            )
            ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.RegexSerDe'
            WITH SERDEPROPERTIES (
            'serialization.format' = '1',
            'input.regex' = 
        '([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*):([0-9]*) ([^ ]*)[:-]([0-9]*) ([-.0-9]*) ([-.0-9]*) ([-.0-9]*) (|[-0-9]*) (-|[-0-9]*) ([-0-9]*) ([-0-9]*) \"([^ ]*) ([^ ]*) (- |[^ ]*)\" \"([^\"]*)\" ([A-Z0-9-]+) ([A-Za-z0-9.-]*) ([^ ]*) \"([^\"]*)\" \"([^\"]*)\" \"([^\"]*)\" ([-.0-9]*) ([^ ]*) \"([^\"]*)\" \"([^\"]*)\" \"([^ ]*)\" \"([^\s]+)\" \"([^\s]+)\"(.*)')
            LOCATION 's3://버킷경로/리전경로?/';



/* 쿼리 */
select * from elb_glowpick_net_logs where elb like '%로드밸런서명%';
```

근데 이게 쿼리당? 비용? 청구하니 좀 더 효율적으로 쿼리 요청해야한다.
```sql 
select type,time,elb,client_ip,client_port,target_ip,target_port,elb_status_code,request_verb,request_url,user_agent from 테이블명 
where regexp_like(elb,'admin')
ORDER BY time desc LIMIT 5;
```


질의 결과

일단 이렇게 나온다는것만 검은색으로 가림은 양해를
![](/assets/imgs/2020/07/08/3.png)

