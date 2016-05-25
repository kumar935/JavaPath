## Migrating Spring MVC to boot: bottom to top approach

- Started with the basic spring boot [setup](http://spring.io/guides/gs/rest-service/)
- Turned into a multi-module project inspired from the olp project.
- `@RestController` vs `@Controller`:   
  `@RestController` = `@Controller` + `@ResponseBody` [SO link](http://stackoverflow.com/a/25242458/3248247) |
  For @ResponseBody, see [this](https://www.genuitec.com/spring-frameworkrestcontroller-vs-controller/)
  `@ResponseBody` alternative `@Produces`
- `@Controller` doesn't seem to be working with boot, this [SO link](http://stackoverflow.com/questions/30406186/spring-boot-java-config-no-mapping-found-for-http-request-with-uri-in) maybe useful.
- Need to get the basics first. [Spring docs](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/overview.html) seem a little too thick. [tutorialspoint](http://www.tutorialspoint.com/spring/index.htm) appears simple. ![spring](http://www.tutorialspoint.com/spring/images/spring_ioc_container.jpg "nice depiction of what spring container does")
  - so beans are just like making new instances of a certain kind of class. See how they used beans [here](http://www.tutorialspoint.com/spring/spring_hello_world_example.htm), in more detail [here](http://www.tutorialspoint.com/spring/spring_bean_definition.htm)
  - 2 types of spring IoC containers: BeanFactory & ApplicationContext, latter being preferred [why?^](http://www.tutorialspoint.com/spring/spring_ioc_containers.htm "The ApplicationContext container includes all functionality of the BeanFactory container, so it is generally recommended over the BeanFactory. BeanFactory can still be used for light weight applications like mobile devices or applet based applications where data volume and speed is significant.")
  - [Bean scopes](http://www.tutorialspoint.com/spring/spring_bean_scopes.htm): Singleton - instantiate once; Prototype - new instance every time.
  - Assigning initializing and destruction callback for bean [link](http://www.tutorialspoint.com/spring/spring_bean_life_cycle.htm)
  - [BeanPostProcessor](http://www.tutorialspoint.com/spring/spring_bean_post_processors.htm): Sequence of stuff: postProcessBeforeInitialization > init-method > postProcessAfterInitialization > method call inside main() > destroy-method
  - Two types of [DI](http://www.tutorialspoint.com/spring/spring_dependency_injection.htm): through constructor and through a setter method, former being recommended on tutorialspoint. Check this p-namespace too, same link.
  - Similar to setter DI, there is [bean injection](http://www.tutorialspoint.com/spring/spring_injecting_inner_beans.htm), you directly assign a bean to the concerned property. 
  - [Autowiring](http://www.tutorialspoint.com/spring/spring_beans_autowiring.htm) : [byName^](http://www.tutorialspoint.com/spring/spring_autowiring_byname.htm "assign property's ref to the bean named same as the propertyName"), [byType^](http://www.tutorialspoint.com/spring/spring_autowiring_bytype.htm "similar to byName, but does matching according to class type"), [byContructor^](http://www.tutorialspoint.com/spring/spring_autowiring_byconstructor.htm "pretty much same as byType, only instead of properties, it is constructor arguments"), and autodetect which first checks byConstructor, which if doesn't work, then byType
  - Using [@Autowired annotation](http://www.tutorialspoint.com/spring/spring_autowired_annotation.htm) on the setter method or the instance of dependency we want to use (which presents itself as a property in the class): basically the same as the byType described above, only we don't have to give the attribute `autowire="byType"` on the bean.
  - [JSR-250 annotations](http://www.tutorialspoint.com/spring/spring_jsr250_annotations.htm) @PostConstruct == init-method attribute & @PreDestroy == destroy-method attribute for the bean. @Resource annotation seems similar to @Autowired, except it takes a 'name' parameter accepting the name of implementation to autowire to. I'm not sure though about @Resource.
  - [Java based configuration](http://www.tutorialspoint.com/spring/spring_java_based_configuration.htm):
    ```java
    @Configuration
    public class HelloWorldConfig {
    
       @Bean 
       public HelloWorld helloWorld(){
          return new HelloWorld();
       }
    }
    ```
    is equivalent to
    ```xml
    <beans>
      <bean id="helloWorld" class="com.tutorialspoint.HelloWorld" />
    </beans>
    ```
    huh. I didn't register the java based beans in the main method as they showed in the tutorial. Maybe that was causing the problem.
      - can use one bean in another just like normal methods
      - will notice `ctx.getBean(abc.class)` instead of `ctx.getBean('abc')` in the examples, that's because when we define beans using annotations, we don't specify `name` as we used to in xml configs.
      - can `@Import` bean definitions, specify `@Bean(initMethod="init", destroyMethod="destroy")` and `@Scope("prototype")`
  - [Events](http://www.tutorialspoint.com/spring/event_handling_in_spring.htm), and [custom events](http://www.tutorialspoint.com/spring/custom_events_in_spring.htm)
  - [AOP](http://www.tutorialspoint.com/spring/schema_based_aop_appoach.htm): Can assign methods to run before, after, after return of a method in the main application using aop, collectively or individually. [@AspectJ](http://www.tutorialspoint.com/spring/aspectj_based_aop_appoach.htm): Same stuff using annotations.
  - [Database interactions using JDBC framework](http://www.tutorialspoint.com/spring/spring_jdbc_framework.htm), [ACID concepts in database](http://www.tutorialspoint.com/spring/spring_transaction_management.htm) (I skipped these)
  - [web.xml and `servlet-name`-servlet.xml^](http://www.tutorialspoint.com/spring/spring_web_mvc_framework.htm "The web.xml file will be kept WebContent/WEB-INF directory of your web application. OK, upon initialization of HelloWeb DispatcherServlet, the framework will try to load the application context from a file named [servlet-name]-servlet.xml located in the application's WebContent/WEB-INF directory. In this case our file will be HelloWeb-servlet.xml.") | `<context:component-scan>`: I think this was what was missing! This lets spring look for `@Controller` | in `[servlet-name]-servlet.xml` beans are created | `InternalResourceViewResolver` for views
