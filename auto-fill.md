# 公共字段自动填充

- 实现元对象处理器接口： com.baomidou.mybatisplus.mapper.IMetaObjectHandler

- 自定义实现类 MyMetaObjectHandler

```java
/**  自定义填充公共 name 字段  */
public class MyMetaObjectHandler  extends MetaObjectHandler {

    /**
     * 测试 user 表 name 字段为空自动填充
     */
    public void insertFill(MetaObject metaObject) {
        // 测试下划线
        Object testType = metaObject.getValue("testType");
        System.err.println("testType==" + testType);
        if (null == testType) {
            metaObject.setValue("testType", 3);
        }
    }

    @Override
    public void updateFill(MetaObject metaObject) {
        //更新填充
    }
}

```

!> 特别说明：** 需要填充的字段需要忽略验证，查看文档问题部分！ **

> spring 启动注入 MyMetaObjectHandler 配置

```xml
<!-- MyBatis SqlSessionFactoryBean 配置 -->
<bean id="sqlSessionFactory" class="com.baomidou.mybatisplus.spring.MybatisSqlSessionFactoryBean">
    <property name="globalConfig" ref="globalConfig"></property>
</bean>
<bean id="globalConfig" class="com.baomidou.mybatisplus.entity.GlobalConfiguration">
    <!-- 公共字段填充处理器 -->
    <property name="metaObjectHandler" ref="myMetaObjectHandler" />
</bean>
<!-- 自定义处理器 -->
<bean id="myMetaObjectHandler" class="com.baomidou.test.MyMetaObjectHandler" />
```
