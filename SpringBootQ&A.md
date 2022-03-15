
### 1) Explain the term ‘Spring Boot’.

It is a Spring module that offers Rapid Application Development to Spring framework. Spring module is used to create an application based on Spring framework which requires to configure few Spring files.

### 2) Mention some advantages of Spring Boot

Here are some major advantages of using spring-boot:
- Easy to understand and develop spring applications.
- Spring Boot is nothing but an existing framework with the addition of an embedded HTTP server and annotation configuration which makes it easier to understand and faster the process of development.
- Increases productivity and reduces development time.
- Minimum configuration.
- We don’t need to write any XML configuration, only a few annotations are required to do the configuration
- Helps you to create a stand-alone application, which can be started using java.jar.
- It offers pinpointed‘started’ POMs to Maven configuration.
- Allows you to Embed Undertow, Tomcat, or Jetty directly.
- Helps you to configure spring whenever possible automatically.
- Provides auto-configuration to load a set of default configuration for a quick start of the application
  ~~Creates stand-alone applications with a range of non-functional features that are common to large classes of projects~~~
  ~~- It comes with embedded tomcat, servlet containers jetty to avoid the usage of WAR files~~
  ~~- Spring Boot provides an opinionated view to reduce the developer effort and simplify maven configurations
-  Provides CLI tool to develop and test applications
- Comes with Spring Boot starters to ensure dependency management and also provides various security metrics
- Consists of a wide range of APIs for monitoring and managing applications in dev and prod.
- Integrates with Spring Ecosystem like Spring JDBC, Spring ORM, Spring Data, Spring Security easily by avoiding boilerplate code.


### Name the features of using Spring Boot
Features of using Spring Boot are:

Starter dependency
Auto-configuration
Spring initializer

### What are the important features of Spring Boot?

Important features of Spring Boot are:

Web Development
Spring Application
Application occasions and listeners
Admin highlights
YAML Support
Type-safe Configuration
Externalized Configuration
Properties Files
Logging and Security

### What are the essential components of Spring Boot

The important components of Spring Boot are:

Spring Boot Starter
Spring Boot autoconfiguration
Spring Boot Actuator
Spring Boot CLI

### What is a Spring Boot Actuator?

Spring Boot Actuator allows you to monitor and manage your application when you want to push it for the production. It helps you to control your application by using HTTP endpoints.

### What is the main difference between JPA and Hibernate?

The main difference between both of them is that JPA is a specification/Interface, whereas Hibernate is only JPA implementations.

### What is a shutdown in the actuator?

A shutdown is an endpoint that helps application to be shut down properly. This feature is not enabled by default.

However, you can use it by setting command: management.endpoint.shutdown.enabled=true in your application.properties file.

### Is it possible to replace or override the Embedded Tomcat server in Spring Boot?

Yes, it is possible to replace the Embedded Tomcat with any other servers by using the starter dependencies. For that, you can use spring-boot-starter-jetty or as a dependency for according you to your need.

### What is @pathVariable?

@PathVariable annotation helps you to extract information from the URI directly.

### 39) What is Swagger2?

Swagger is used to describing the structure of APIs. Swagger 2 is an open-source service provided in Spring Boot which makes it easier for the machines to find out the structure of APIs like RESTful Web services.

### What are different environments for enterprise application development?

Dev
QA
Stage
Production
### What are the major differences between RequestMapping and GetMapping?

RequestMapping can be used with GET, POST, PUT, and many other request methods using the method attribute on the annotation. Whereas GetMapping is only an extension of RequestMapping, which helps you to improve clarity on requests.

### How can you define properties in Spring Boot?

You can define properties in Spring Boot with the help of the application.properties file which exists in a classpath of the application as follows.

### How to create a Spring Boot project using Maven?

Use any of the following methods to create a project.

Spring Initializr
Spring Boot CLI
Spring Starter Project Wizard
### What is the use of profiles in Spring Boot?

Profiles are used to separate various parts of your spring application configuration and make it only available in certain environments.

### Explain Auto-Configuration in Spring Boot.

Auto-configuration is used to configure Spring application automatically based on dependencies of classpath parameter. It makes development faster and easier.

### What is the meaning of Aspect-Oriented Programming (AOP)?

Aspect-Oriented Programming supplements Object-Oriented Programming that aims to increase modularity. AOP breaks program logic into various parts, which are called concerns.

### What is Cross-Site Request Forgery attack?

Cross-Site Request Forgery attack or one-click attack is an attack that forces other users to execute malicious commands on the application. CSRF attack specifically targets state-changing requests.

### Explain CORS in Spring Boot?

CORS stands for Cross-Origin Resource Sharing is a  mechanism implemented by browsers and helps users to authorize cross-domain requests. This mechanism serves as an alternative to less secure and less powerful hacks of the kinds of IFrame or JSONP.

### What do you understand by auto-configuration in Spring Boot and how to disable the auto-configuration?
Auto-configuration is used to automatically configure the required configuration for the application. For example, if you have a data source bean present in the classpath of the application, then it automatically configures the JDBC template. With the help of auto-configuration, you can create a Java application in an easy way, as it automatically configures the required beans, controllers, etc. 

To disable the auto-configuration property, you have to exclude attribute of @EnableAutoConfiguration, in the scenario where you do not want it to be applied.

1
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
If the class is not on the classpath, then to exclude the auto-configuration, you have to mention the following code:

1
@EnableAutoConfiguration(excludeName={Sample.class})
Apart from this, Spring Boot also provides the facility to exclude list of auto-configuration classes by using the spring.autoconfigure.exclude property. You can go forward, and add it either in the application.properties or add multiple classes with comma-separated.

### Mention the advantages of the YAML file than Properties file and the different ways to load YAML file in Spring boot.
The advantages of the YAML file than a properties file is that the data is stored in a hierarchical format. So, it becomes very easy for the developers to debug if there is an issue. The SpringApplication class supports the YAML file as an alternative to properties whenever you use the SnakeYAML library on your classpath. The different ways to load a YAML file in Spring Boot is as follows:

Use YamlMapFactoryBean to load YAML as a Map
Use YamlPropertiesFactoryBean to load YAML as Properties

# Explain how to register a custom auto-configuration.
In order to register an auto-configuration class, you have to mention the fully-qualified name under the **@EnableAutoConfiguration key META-INF/spring. factories file. Also, if we build the with maven, then this file should be placed in the resources/META-INT directory. **

# How to instruct an auto-configuration to back off when a bean exists?
To instruct an auto-configuration class to back off when a bean exists, you have to use the @ConditionalOnMissingBean annotation. The attributes of this annotation are as follows:

value: This attribute stores the type of beans to be checked
name: This attribute stores the name of beans to be checked
