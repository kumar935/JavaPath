## Migrating Spring MVC to boot

- Started [here](http://docs.spring.io/spring-boot/docs/current/reference/html/howto-traditional-deployment.html#howto-convert-an-existing-application-to-spring-boot), and [StackOverflow link](http://stackoverflow.com/questions/31409231/migrate-existing-spring-app-to-spring-boot-manually-configure-spring-boot)
    - ApplicationContext: [spring doc](https://spring.io/understanding/application-context)
- Or, [here](https://github.com/spring-projects/spring-boot/issues/137), it led to [stackoverflow link](http://stackoverflow.com/questions/20240939/how-to-migrate-from-traditional-java-web-application-with-web-xml-to-spring-boot)
    - Need to know whether we want jar or war
        - need to understand build process. [spring doc](https://spring.io/guides/gs/maven/)
        - mvn package vs install, [source](https://spring.io/guides/gs/maven/)
            > Maven also maintains a repository of dependencies on your local machine (usually in a .m2/repository directory in your home directory) for quick access to project dependencies. If you’d like to install your project’s JAR file to that local repository, then you should invoke the install goal: `mvn install`. The install goal will compile, test, and package your project’s code and then copy it into the local dependency repository, ready for another project to reference it as a dependency.
    - Understand web.xml: Kind of like an interceptor for requests. It's ultimately here that the request is sent to the DispatcherServlet, hence the controllers.
    - So apparently Application.java of spring boot is going to do the job of web.xml, and we need to kind of translate web.xml into Application.java? [stackoverflow link](http://stackoverflow.com/a/22408998/3248247)





