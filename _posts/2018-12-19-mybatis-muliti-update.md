---

title: mybatis muliti update 하려면! 
published: true
---

mybatis muliti update 하려면~!

```
<update id="Mapper메서드명" parameterType="java.util.List">
   <foreach item="temp" index="index" collection="list" open="" close="" separator=";">
      UPDATE 테이블
      SET 컬럼 = #{temp.test1}
      WHERE 컬럼 = #{temp.test2}
   </foreach>
</update>
```


```
sudo service nginx start

```

application.yml에서 

jdbc.allowMultiQueries=true

되어 있어야 멀티업데이트가 된다.

요즘엔 JPA로 하고 있어서 잘안쓰지만 예전에 한참 Mybatis를 이용해서 플젝했을때는 종종쓴거 같다~