依赖注入降低耦合便于管理关系  
在beans.xml中注明关系  
避免出现硬编码

``` javascript
enter code here
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--在配置文件当中描述bean的关系，降低耦合-->
    <!--
        注入数据的类型
            基本类型和string
            其他bean类型
            复杂类型/集合类型
        注入方式
            使用构造函数
            使用set方法
            使用注解提供（在后面）
    -->
    <!--构造函数注入
        标签：constructor-arg
            type、index、name根据类型，索引，名字给指定的参数赋值
            value:用于提供基本类型和string类型的数据
            ref:用于指定其他的bean类型的数据
        构造函数每个属性都要注入，不够灵活，
    <bean id="accountService" class="com.service.AccountService">
        <constructor-arg name="name" value="111"></construtor-arg>
        <constructor-arg name="birthdat" ref="now"></construtor-arg>

    </bean>
        <bean id="now" class="java.util.Data"></bean>
        -->
    <!--
        set方法注入 更常用的方式
        property
        name:用于指定注入是set方法除去set的名称
        value:用于指定其他类型的数据
        更加灵活，但可能测试不全面
        具体不再展示

    -->
    <!--
    复杂类型的注入、集合注入
        list、map、set、array、props
        <bean id="accountService" class="com.service.accountservice" >
            <property name="myset">
                <set>
                    <value>AAA</value>
                    <value>BBB</value>
                </set>
            </property>
           <property name="myarray">
                <array>
                    <value>AAA</value>
                    <value>BBB</value>
                 </array>
           </property>
           <property name="mylist">
                <list>
                    <value>AAA</value>
                    <value>BBB</value>
                 </list>
           </property>
           <property name="myprops">
                <props>
                    <prop key="test1">AAA</prop>
                    <prop key="test2" >BBB</prop>
                 </props>
           </property>
            <property name="myprops">
                <map>
                    <entry key="testA" value="AAA"></entry>
                    <entry key="testB">
                        <value>bbb</value>
                    </entry>
                 </map>
           </property>
    -->
</beans>
```
程序员八荣八耻中  
以可配置为荣 ，以硬编码为耻
