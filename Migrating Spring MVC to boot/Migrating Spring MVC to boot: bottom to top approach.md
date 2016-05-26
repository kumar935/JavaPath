## Migrating Spring MVC to boot: bottom to top approach

- Started with the basic spring boot [setup](http://spring.io/guides/gs/rest-service/)
- Turned into a multi-module project inspired from the olp project.
- `@RestController` vs `@Controller`:   
  `@RestController` = `@Controller` + `@ResponseBody` [SO link](http://stackoverflow.com/a/25242458/3248247) |
  For @ResponseBody, see [this](https://www.genuitec.com/spring-frameworkrestcontroller-vs-controller/)
  `@ResponseBody` alternative `@Produces`
- `@Controller` doesn't seem to be working with boot, this [SO link](http://stackoverflow.com/questions/30406186/spring-boot-java-config-no-mapping-found-for-http-request-with-uri-in) maybe useful.
- Need to get the basics first. Covered that [here](https://github.com/kumar935/JavaPath/blob/master/03%20spring/04%20spring-tutorialspoint.md)
- ViewResolver error [SO link](http://stackoverflow.com/questions/29953245/configure-viewresolver-with-spring-boot-and-annotations-gives-no-mapping-found-f): Also see how configuration class is written. Keep the configuration class in the same directory as `Application.java`.
- So everything works great with `@Controller` + `@ResponseBody` or `@RestController` and `@RequestMapping`, but `@Controller` and `@Path` are making the app look for a view on the requested path. `@Path` is a part of Jersey, which I think I should give a look what it is. I'm probably missing some configuration related to it. And here it is: [link](https://dzone.com/articles/using-jax-rs-with-spring-boot-instead-of-mvc). It works! finally!! ^_^
