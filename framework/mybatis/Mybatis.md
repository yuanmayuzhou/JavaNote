# Mybatis

### Mybatis��#��$������
'#'���൱�ڶ����ݼ���˫���Ŵ��룬'$'���൱����ֱ��ƴ���ַ����ķ�ʽƴ�Ӵ��������

'$'һ������ƴ�Ӷ�̬��������̬�ֶε����

���û��˴���Ĳ���һ����'#'���գ���Ϊ'$'��ֻ���ڿ���м򵥵Ķ�SQL����ƴ�ӣ��޷���ֹ�����SQLע�룬��'#'�ŵ�ͬ��JDBC�е�'?'��ռλ�����ܹ��ܴ�̶��ϱ���SQLע��

### Mybatis�ı�̲�����ʲô���ģ�
1.����SqlSessionFactory

2.ͨ��SqlSessionFactory����SqlSession

3.ͨ��sqlsessionִ�����ݿ����

4.����session.commit()�ύ����

5.����session.close()�رջỰ

### Mybatis�е�һ������Ͷ������棿
һ������ΪSqlSession����Ļ��棬Ĭ�Ͽ�������һ��SqlSession�Ự�У���һ�β�ѯʱ�Ὣ���ݻ��浽�ڴ��У�һ��Map�ṹ����MappedStatement��ȫ����+���õķ�����������������ҳ��Ϣ����Key����ѯ���������ݶ���ΪValue�����ڶ���ִ��ͬ���Ĳ�ѯʱ����ֱ�Ӵ��ڴ���ȡ����ֻ�н������޸ģ�ɾ�������Ӵ���������ʱ����commit��closeʱ�Ż���ջ��档

���������л���������ݣ������Ƕ��󣬶�������Ĭ�ϲ���������������������Ҫ��mybatis��cacheEnabled����Ϊtrue��������xml�ļ��н�ִ�е�sql���������useCache="true"������������һ��SqlSessionFactory����Ļ��棬ֻҪ��һ��SqlSessionFactory������SqlSession������һ���������棬�����ж�������ʱ��ͨ���洢�����ݹ������ݶ��󷵻أ���ѯ����ʱ�Ĳ�ѯ˳��Ϊ���������� -> һ������ -> ���ݿ⡣

### MyBatis��insert�������ʱ��η�������ID��
���ݿ�Ϊ MySql ʱ��
```java
<insert id="insert" parameterType="com.test.User" keyProperty="userId" useGeneratedKeys="true">
```
��keyProperty����ʾ���ص�idҪ���浽����������У���useGeneratedKeys����ʾ����idΪ������ģʽ��

���ݿ�ΪOracleʱ��
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
����Oracleû����������һ˵����ֻ������������������ʽ�����Բ�����ʹ�á�useGeneratedKeys�����ԡ�����ʹ��<selectKey>��ID��ȡ����ֵ������������У�insert�������ʱ��������id��

### ʹ��MyBatis��mapper�ӿڵ���ʱ����ЩҪ��
1.Mapper�ӿڷ�������mapper.xml�ж����ÿ��sql��id��ͬ

2.Mapper�ӿڷ���������������ͺ�mapper.xml�ж����ÿ��sql��parameterType��������ͬ

3.Mapper�ӿڷ���������������ͺ�mapper.xml�ж����ÿ��sql��resultType��������ͬ

4.Mapper.xml�ļ��е�namespace����mapper�ӿڵ���·��
