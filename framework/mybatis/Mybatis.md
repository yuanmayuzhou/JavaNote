# Mybatis

### Mybatis中#和$的区别？
'#'号相当于对数据加上双引号传入，'$'号相当于以直接拼接字符串的方式拼接传入的数据

'$'一般用于拼接动态表名，动态字段等情况

从用户端传入的参数一般用'#'接收，因为'$'号只是在框架中简单的对SQL进行拼接，无法防止恶意的SQL注入，而'#'号等同于JDBC中的'?'号占位符，能够很大程度上避免SQL注入

### Mybatis的编程步骤是什么样的？
1.创建SqlSessionFactory

2.通过SqlSessionFactory创建SqlSession

3.通过sqlsession执行数据库操作

4.调用session.commit()提交事务

5.调用session.close()关闭会话

### Mybatis中的一级缓存和二级缓存？
一级缓存为SqlSession级别的缓存，默认开启，在一个SqlSession会话中，第一次查询时会将数据缓存到内存中，一个Map结构，由MappedStatement（全限名+调用的方法名）、参数、分页信息构成Key，查询出来的数据对象为Value，当第二次执行同样的查询时，将直接从内存中取出，只有进行了修改，删除，增加此类变更操作时，或commit，close时才会清空缓存。

二级缓存中缓存的是数据，而不是对象，二级缓存默认不开启，开启二级缓存需要将mybatis的cacheEnabled配置为true，并且在xml文件中将执行的sql语句配置上useCache="true"。二级缓存是一个SqlSessionFactory级别的缓存，只要由一个SqlSessionFactory产生的SqlSession都共享一个二级缓存，当命中二级缓存时，通过存储的数据构造数据对象返回，查询数据时的查询顺序为：二级缓存 -> 一级缓存 -> 数据库。

### MyBatis在insert插入操作时如何返回主键ID？
数据库为 MySql 时：
```java
<insert id="insert" parameterType="com.test.User" keyProperty="userId" useGeneratedKeys="true">
```
“keyProperty”表示返回的id要保存到对象的属性中，“useGeneratedKeys”表示主键id为自增长模式。

数据库为Oracle时：
```java
<insert id="insert" parameterType="com.test.User">
    <selectKey resultType="INTEGER" order="BEFORE" keyProperty="userId">
        SELECT SEQ_USER.NEXTVAL as userId from DUAL
    </selectKey>
    insert into user 
        (user_id, user_name, modified, state)
    values 
        (#{userId,jdbcType=INTEGER}, #{userName,jdbcType=VARCHAR}, #{modified,jdbcType=TIMESTAMP},#{state,jdbcType=INTEGER})
</insert>
```
由于Oracle没有自增长这一说法，只有序列这种自增的形式，所以不能再使用“useGeneratedKeys”属性。而是使用<selectKey>将ID获取并赋值到对象的属性中，insert插入操作时正常插入id。

### 使用MyBatis的mapper接口调用时有哪些要求？
1.Mapper接口方法名和mapper.xml中定义的每个sql的id相同

2.Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql的parameterType的类型相同

3.Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同

4.Mapper.xml文件中的namespace即是mapper接口的类路径
