### IOC Container 
IOC containers are implemented using two ways:
1. BeanFactory (Basic Feature) Only to be used when memory consumption is critical. (As of Spring 2.0, XmlBeanFactory is deprecated and using ApplicationContext is recommended.)
```
import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;

public class BeanFactoryExample {
    public static void main(String[] args) {
        // Create the BeanFactory using an XML configuration file
        BeanFactory beanFactory = new XmlBeanFactory(new ClassPathResource("beans.xml"));

        // Retrieve a bean from the factory
        MyBean myBean = (MyBean) beanFactory.getBean("myBean");
        
        // Use the bean
        myBean.doSomething();
    }
}
```
2. ApplicationContext (Advanced Feature) preferrable to be used. 
ApplicationContext is the extended version of BeanFactory as It extends ListableBeanFactory which further extends BeanFactory.
```
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ApplicationContextExample {
    public static void main(String[] args) {
        // Create the ApplicationContext using an XML configuration file
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

        // Retrieve a bean from the context
        MyBean myBean = (MyBean) context.getBean("myBean");

        // Use the bean
        myBean.doSomething();
    }
}
```
```
// bean.xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
                           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myBean" class="com.example.MyBean" />
</beans>
```
```
// XML Based
     ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("Config.xml");
      // It would return the application context and would look for Config.xml and will create bean on the basis of it.
     Object bean = context.getBean("IdDefinedInConfigxml", ClassFileName.class);
     bean.callMethodWhichIsInsideTheBean();
```
### Bean Life Cycle 
Bean Instantiation  >> Populate Properties  >> BeanNameAware.setBeanName() >> BeanFactoryAware.setBeanFactory()  >>  ApplicationContextAware.setApplicationContext() >>
 postProcessBeforeInitialization() (BeanPostProcessor)  >> InitializingBean.afterPropertiesSet()  >>    Custom Init Method  >> postProcessAfterInitialization() (BeanPostProcessor)  >> Bean Ready to Use   >> Container Shutdown   >> DisposableBean.destroy() >> Custom Destroy 
                                                                                 OR
Container Started >> Bean Instantiated >> Dependency Injected >> Bean Instantiated >>  Custom Init Method >> Bean Destroyed Or IOC Container Closed >> Custom Destoy Method 
### Scope of Bean
There are 6 scope of Bean but last 4 are limited to web aware application or web application context.
1. Singleton (Single shared instance)
2. Prototype (New instance for each request and destructionis managed by client not IOC)
3. Request (new instance of the bean is created for each HTTP request)
4. Session (one instance is created for multiple HTTP requests within a single session, once session ends bean gone)
5. Application (Created for the lifecycle of a ServletContext and exist during the entire lifecycle of the web application)
6. Global Session Scope (Maintain state across multiple HTTP requests and across multiple portlets within a global session.)

|   Question | Command |
| --- | ----------- |
|Dependency Injection| It can be done using three ways: constructor injection, settor injection and field injection. In case of constructor and setter injection we annotate the constructor and setter with @Autowired which would be ultimately assigning value to the current instance after taking it as the aurgument. Remember, this setter and constructor are used by Spring IOC container internally for the dependency injection.|
| @Autowired | It checks for all the class which implements the interface annotated with @Autowired and has @Component as annotation to find the implementation and to inject it | 
|@Qualifier("beanid")| It is used to resolve bean conflict for autowiring and It is placed above the @Autowired|
|Bean ID| Spring takes the class name as the bean id, If it is not defined. Just it makes the first letter small.|
|@ComponantScan("BasePackageName")|Earlier in case of Spring Core, we have been using config.xml wherein we have been managing name of application.properperties and the name of base package. This was discarded by annotation @ComponentScan which checks for all the class with @Component and register bean into IOC|
|@Configuration| It is the replacement of config.xml in spring boot. If we want to define bean without using @Component then we can explicitly define beans inside this class which has been annotated with @Configuration and can annotate bean with @Bean|
|@PropertySource("DemoApplication.properties")| As we happened to define app.properties name in the config.xml. Herein, using this @PropertySource we can define the name directly using annotation|
|||

### Transaction Management
|   Annotation | Description |
| --- | ----------- |
|@Transactional|By default, the transaction will roll back on runtime exceptions (unchecked exceptions) and errors. It will not roll back on checked exceptions.|
|@Transactional(rollbackFor = Exception.class)|You can specify which exceptions should cause a rollback using the rollbackFor attribute.|
|@Transactional(noRollbackFor = CustomException.class)|Use the noRollbackFor attribute to specify exceptions that should not cause a rollback.|
|PlatformTransactionManager|If you need more control over the transaction then go for it | 
```
    @Autowired
    private PlatformTransactionManager transactionManager;
TransactionDefinition def = new DefaultTransactionDefinition();
TransactionStatus status = transactionManager.getTransaction(def);
transactionManager.commit(status);
transactionManager.rollback(status);
```
|   @Transactional Attributes | Description |
| --- | ----------- |
|PROPAGATION_REQUIRED: |Support a current transaction; create a new one if none exists.|
|PROPAGATION_REQUIRES_NEW:| Create a new transaction, suspending the current transaction if one exists.|
|PROPAGATION_MANDATORY:| Support a current transaction; throw an exception if no current transaction exists.|
|PROPAGATION_NOT_SUPPORTED:| Execute non-transactionally, suspending the current transaction if one exists.|
|PROPAGATION_NEVER: |Execute non-transactionally; throw an exception if a transaction exists.|
|PROPAGATION_NESTED:| Execute within a nested transaction if a current transaction exists.|
|ISOLATION_DEFAULT:| Use the default isolation level of the underlying database.|
|ISOLATION_READ_UNCOMMITTED:| Allow reading uncommitted changes.|
|ISOLATION_READ_COMMITTED:| Prevent dirty reads; allow non-repeatable reads and phantom reads.|
|ISOLATION_REPEATABLE_READ:| Prevent dirty reads and non-repeatable reads; allow phantom reads.|
|ISOLATION_SERIALIZABLE:| Prevent dirty reads, non-repeatable reads, and phantom reads.|
|TIMEOUT_DEFAULT:| Use the default timeout of the underlying transaction system.|
|TIMEOUT:| Specify a custom timeout.|
|readOnly:| Indicate whether the transaction is read-only.|

If we are using requires new then a new transaction will be created, we can use it for retry mechanism which would be independent of current transaction. 

### Important Terminology
|   Term | Description |
| --- | ----------- |
|@RequestParam String name | "/greet?name=John" |
|@QueryParam("name") String name| "/greet?name=John" It is part of JAX-RS and same as @RequestParam|
|@PathVariable String name| "/greet/John" (Placeholder needs to be defined in @GetMapping(/api/{name}))|


