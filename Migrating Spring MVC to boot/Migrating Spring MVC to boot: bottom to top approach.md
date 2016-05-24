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
  - [Autowiring](http://www.tutorialspoint.com/spring/spring_beans_autowiring.htm) : [by propertyName](http://www.tutorialspoint.com/spring/spring_autowiring_byname.htm) (assign property's ref to the bean named same as the propertyName)
