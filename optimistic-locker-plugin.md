# 乐观锁插件

## 插件配置

```xml
<bean class="com.baomidou.mybatisplus.plugins.OptimisticLockerInterceptor">
  <property name="properties">
    <value>
      versionHandlers=com.baomidou.mybatisplus.test.plugins.optimisticLocker.StringTypeHandler
    </value>
  </property>
</bean>
```

## 注解实体

```java
public class user {
    @Version
    private Integer version;

    ...
}
```

!> 特别说明： **注解一定要有！支持字段类型查看 OptimisticLockerInterceptor 源码说明**
