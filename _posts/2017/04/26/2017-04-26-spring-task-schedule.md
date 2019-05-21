---

title: Spring 태스크(Task) 네임스페이스
layout: post 
category: spring 
tags: 
  - spring
  - task
  - schedule
---

Spring 태스크(Task) 네임스페이스
---------------------------------------------

스프링 3.0부터 TaskExecutor와 TaskScheduler 인스턴스를 구성하는 XML 네임스페이스가 존재하고 트리거로 예약된 태스크를 구성하는 간편한 방법도 제공

XML 설정

```
xmlns:task="http://www.springframework.org/schema/task"
```

```
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.1.xsd
        http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-3.1.xsd"
```

[Spring Scheduling 참조](http://dev.anyframejava.org/docs/anyframe/plugin/scheduling/4.5.2/reference/html/ch02.html) task Namespace의 가장 강력한 특징인 task:scheduled-task/를 사용한 속성 정의의 일부이다.

task:scheduled-task/는 기본적으로 'scheduler'라는 속성을 가지고 있는데 이것은 내부에 정의된 Task를 Scheduling하기 위한 TaskScheduler Bean을 정의하기 위한 것이다.

task:scheduled-task/는 하위에 다수의 task:scheduled/를 포함할 수 있으며 task:scheduled/의 'ref'와 'method'는 실행 대상이 되는 Bean과 해당 Bean 내에 포함된 실행 대상 메소드를 정의하기 위한 속성이다.

```
<task:scheduled-tasks scheduler="scheduler">
    <task:scheduled ref="task" method="printWithFixedDelay" fixed-delay="5000"/>
    <task:scheduled ref="task" method="printWithFixedRate" fixed-rate="10000"/>
    <task:scheduled ref="task" method="printWithCron" cron="*/8 * * * * MON-FRI"/>
</task:scheduled-tasks>

<task:scheduler id="scheduler" pool-size="10"/>
```
