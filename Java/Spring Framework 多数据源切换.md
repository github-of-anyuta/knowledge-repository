
Spring Framework 多数据源切换
=============================

## 1. 创建动态数据源对象

```java
public class DynamicDataSource extends AbstractRoutingDataSource {
    
    public static final String DATASOURCE_DS1 = "ds1DataSource";
    
    public static final String DATASOURCE_DS2 = "ds2DataSource";
    
    public static final String DATASOURCE_DEFAULT = DATASOURCE_DS1;
    
    private static final ThreadLocal<String> dataSourceLoc = new ThreadLocal<String>();

    public static void setDataSource(String dataSource) {
        dataSourceLoc.set(dataSource);
    }

    @Override
    protected Object determineCurrentLookupKey() {
        String currentDataSource = dataSourceLoc.get();
        if (DataUtil.isEmpty(currentDataSource, true)) {
            currentDataSource = DATASOURCE_DEFAULT;
            dataSourceLoc.set(currentDataSource);
        }
        return currentDataSource;
    }
}
```

## 2. 配置 applicationContext-dataSource.xml 数据源

```xml
<bean id="ds1DataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close" scope="singleton">
    <property name="driverClassName" value="${mysql.driverClassName}" />
    <property name="url" value="${mysql.url}" />
    <property name="username" value="${mysql.username}" />
    <property name="password" value="${mysql.password}" />
    <property name="validationQuery" value="SELECT 1" />
    ...
</bean>

<bean id="ds2DataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close" scope="singleton">
    <property name="driverClassName" value="${oracle.driverClassName}" />
    <property name="url" value="${oracle.url}" />
    <property name="username" value="${oracle.username}" />
    <property name="password" value="${oracle.password}" />
    <property name="validationQuery" value="SELECT 1" />
    ...
</bean>

<bean id="dataSource" class="com.test.DynamicDataSource">
    <property name="defaultTargetDataSource" ref="ds1DataSource"/>
    <property name="targetDataSources">
        <map>
            <entry key="ds1DataSource" value-ref="ds1DataSource"/>
            <entry key="ds2DataSource" value-ref="ds2DataSource"/>
        </map>
    </property>
</bean>
```
