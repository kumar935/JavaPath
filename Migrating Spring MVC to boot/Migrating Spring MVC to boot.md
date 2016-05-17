## Migrating Spring MVC to boot

- Started [here](http://docs.spring.io/spring-boot/docs/current/reference/html/howto-traditional-deployment.html#howto-convert-an-existing-application-to-spring-boot), and [StackOverflow link](http://stackoverflow.com/questions/31409231/migrate-existing-spring-app-to-spring-boot-manually-configure-spring-boot)
    - ApplicationContext: [spring doc](https://spring.io/understanding/application-context)
- Or, [here](https://github.com/spring-projects/spring-boot/issues/137), it led to [stackoverflow link](http://stackoverflow.com/questions/20240939/how-to-migrate-from-traditional-java-web-application-with-web-xml-to-spring-boot)
    - Need to know whether we want jar or war
        - need to understand build process. [spring doc](https://spring.io/guides/gs/maven/)
        - mvn package vs install, [source^](https://spring.io/guides/gs/maven/ "Maven also maintains a repository of dependencies on your local machine (usually in a .m2/repository directory in your home directory) for quick access to project dependencies. If you’d like to install your project’s JAR file to that local repository, then you should invoke the install goal: `mvn install`. The install goal will compile, test, and package your project’s code and then copy it into the local dependency repository, ready for another project to reference it as a dependency.")
        - Difference between plugin and dependency in pom.xml: [StackOverflow link](http://stackoverflow.com/questions/11881663/what-is-the-difference-in-maven-between-dependency-and-plugin-tags-in-pom-xml)
    - Understand web.xml: Kind of like an interceptor for requests. It's ultimately here that the request is sent to the DispatcherServlet, and subsequently, the controllers.
    - So apparently Application.java of spring boot is going to do the job of web.xml, and we need to kind of translate web.xml into Application.java? [stackoverflow link](http://stackoverflow.com/a/22408998/3248247)
        - First, need to add spring boot dependency in the project pom:
            - in the outermost pom, added parent as spring-boot-starter-parent, as in the pom [here](http://spring.io/guides/gs/spring-boot/). And also in the pom of the entrypoint project, add suitable plugins and dependencies
        - Now, transferring web.xml's work:
            - `<display-name>`: add application.properties in the resources directory [properties list](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)
            - `<context-param>`: easy peasy, check this [link](http://stackoverflow.com/a/26648258/3248247)
            - `<listener>` [StackOverflow source](http://stackoverflow.com/a/28566481/3248247):
                - for ContextLoaderListener (similar for other listeners):
                    ```java
                    @Bean
                    @ConditionalOnMissingBean(ContextLoaderListener.class)
                    public ContextLoaderListener requestContextListener() {
                        return new ContextLoaderListener();
                    }
                    ```
            - `<filter>`: Stackoverflow: [1](http://stackoverflow.com/a/30658752/3248247), [2](http://stackoverflow.com/a/19830906/3248247), example: [3](http://stackoverflow.com/a/28214811/3248247)
            - `<servlet>`: [StackOverflow link](http://stackoverflow.com/a/22408998/3248247)
            - `<session-config>` stuff in application.properties: [appendix](http://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)
            - Can get error regarding conflicts in implementations of logging library, see [here](http://stackoverflow.com/questions/23984009/disable-logback-in-springboot), in my case I just had the sequence of dependencies wrong. The spring boot dependency should be at the top.






