### IOC Container 
IOC containers are implemented using two ways:
1. BeanFactory (Basic Feature) Only to be used when memory consumption is critical.
2. ApplicationContext (Advanced Feature) preferrable to be used. 
ApplicationContext is the extended version of BeanFactory as It extends ListableBeanFactory which further extends BeanFactory.
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


