---

title: Java Json library jackson 사용법
published: true
comments : true
---


## 개요

Jackson 은 자바용 json 라이브러리로 잘 알려져 있지만 Json 뿐만 아니라 XML/YAML/CSV 등 다양한 형식의 데이타를 지원하는 data-processing 툴이다. 스트림 방식이므로 속도가 빠르며 유연하며 다양한 third party 데이타 타입을 지원하며 annotation 방식으로 메타 데이타를 기술할 수 있으므로 JSON 의 약점중 하나인 문서화와 데이타 validation 문제를 해결할 수 있다.

- Annotation 1.@JsonIgnoreProperties 2.@JsonProperty 3.@JsonInclude

## @JsonIgnoreProperties
크게 2가지 용도가 있으며 첫 번째는 Serializer/Deserialize 시 제외시킬 프로퍼티를 지정한다. 다음과 같이 지정하면 foo, bar는 제외된다. 개별 프로퍼티를 제외하려면 @JsonIgnore annotation을 프로퍼티에 적용하면 된다.

```
@JsonIgnoreProperties({ "foo", "bar" })
public class MyBean
{
   //아래 두 개는 제외됨.
   public String foo;
   public String bar;

   // will not be written as JSON; nor assigned from JSON:
   @JsonIgnore
   public String internal;

   // no annotation, public field is read/written normally
   public String external;

   @JsonIgnore
   public void setCode(int c) { _code = c; }

   // note: will also be ignored because setter has annotation!
   public int getCode() { return _code; }
}
```


## @JsonProperty
getter/setter 의 이름을 property 와 다른 이름을 사용할 수 있도록 설정한다. Database 를 자바 클래스로 매핑하는데 DB의 컬럼명이 알기 어려울 경우등에 유용하게 사용할 수 있다. 다음과 같은 테이블이 있을 경우

```
CREATE TABLE Users (
  u INT NOT NULL,
  a INT NOT NULL,
  e VARCHAR(80) NOT NULL
);
```
다음과 같이 JsonProperty 를 사용하면 DB 의 컬럼명을 변경하지 않아도 가독성을 높일 수 있다.
```
public class User
{
    @JsonProperty("userId");
    public Integer u;

    @JsonProperty("age");
    public Integer a;

    @JsonProperty("email");
    public String e;
}

```
json 으로 변환된 결과

```
{
    "userId": 1,
    "age": 13,
    "email": "user@host.com"
}
```

## @JsonInclude
Serialize 시 동작을 지정한다. 기본적으로 잭슨은 값의 유무와 상관없이 무조건 serialize 하게 되지만 다음과 같이 설정할 경우 not null 이거나 none empty 일 경우에만 serialize 된다.

```
public class User
{
    public Integer u;

    @JsonInclude(Include.NON_NULL)
    public Integer age;


    @JsonInclude(Include.NON_EMPTY)
    public String email;
}
```
