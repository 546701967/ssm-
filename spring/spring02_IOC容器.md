通过上个笔记的工厂管理类很容易理解ioc容器  
meven项目导入spring包  
``` 
<dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.0.2.RELEASE</version>
        </dependency>

```
spring IOC容器管理bean对象  

``` javascript
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
  <!--spring管理bean -->
        <!-- 创建bean的三种方式
            bean对象的作用范围
            bean对象的生命周期
        -->

        <!-- 使用默认构造函数创建
            在spring的配置文件中使用bean标签，填写必须的id,class属性后，没有其他属性和标签，默认才用的就是默认构造函数
            <bean id="accountService" class="com.service.AccountService"></bean>
        -->
        <!--使用普通工厂中的方法创建对象//这种方法一般在使用第三方jar包时使用，因为不清楚第三方jar包是否有构造函数
            <bean id="instanceFactory" class="com.factor.InstanceFactory"></bean>
            <bean id="accountService" factory-bean="instanceFactory" factory-mathod="getAccountService"></bean>
            //===========
            public class InstanceFactory {
            public IAccountService getAccountService(){
                return new AccountServiceImpl();
                }
            }

        -->
        <!--
        <bean id="accountService" class="com.factory.StaticFactory" factory-method="getAccountService"></bean>
        //===========
            public class StaticFactory {
            public static IAccountService getAccountService(){
            return new AccountServiceImpl();
                }
            }
        -->
        <!--
            bean标签的scope属性
            指定bean的作用范围(类型)
            取值
                singleton:单例的 默认值
                prototype:多例的
                request: 作用于web应用的请求范围
                session: 作用于web应用的会话范围
                global-session: 作用于集群环境的会话范围，非集群范围就等于session
         <bean id="accountService" class="com.service.accountService" scope=""></bean>


        -->
    <!--
        bean对象的生命周期
        单例对象的生命周期
        多例对象的生命周期
        不再赘述，跟非bean容器管理时一样，理解单例和多例就清楚生命周期

    -->
```
从spring IOC容器中取出bean对象  

``` javascript
/**
 * 获取spring的ioc核心容器，并根据id获取对象
 * Applicationcontext的三个常用实现类
 *      ClassPathXmlApplicationContext: 他可以加载类路径下的配置文件
 *      FileSystemXmlApplicationContext: 加载磁盘上仁义路径下的配置文件
 *      AnnotationConfigApplicationContext:根据注解创建容器
 *
 *      ApplicationContext 立即加载 功能多 一般使用
 *      BeanFactory 延迟加载 功能少，在轻量级应用中使用
 *
 */
public class Client {
    public static void main(String[] args) {
        //AccountService accountService = (AccountService) BeanFactory.getBean("accountService");
        //accountService.saveAccount();
        ApplicationContext ac=new ClassPathXmlApplicationContext("bean.xml");
        IAccountService as= (IAccountService)ac.getBean("accountService");
        IAccountDao adao = ac.getBean("accountDao",IAccountDao.class);
    }
}
```
