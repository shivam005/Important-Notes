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
