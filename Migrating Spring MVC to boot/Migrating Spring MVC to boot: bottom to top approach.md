## Migrating Spring MVC to boot: bottom to top approach

- Started with the basic spring boot [setup](http://spring.io/guides/gs/rest-service/)
- Turned into a multi-module project inspired from the olp project.
- `@RestController` vs `@Controller`:   
  `@RestController` = `@Controller` + `@ResponseBody` [SO link](http://stackoverflow.com/a/25242458/3248247) |
  For @ResponseBody, see [this](https://www.genuitec.com/spring-frameworkrestcontroller-vs-controller/)
  `@ResponseBody` alternative `@Produces`
- `@Controller` doesn't seem to be working with boot, this [SO link](http://stackoverflow.com/questions/30406186/spring-boot-java-config-no-mapping-found-for-http-request-with-uri-in) maybe useful.
- Need to get the basics first. Covered that [here](https://github.com/kumar935/JavaPath/blob/master/03%20spring/04%20spring-tutorialspoint.md)
