
# Explain the concept of the Dispatcher Servlet.

Answer: Dispatcher Servlet is the main central servlet that handles all the incoming HTTP Request and Responses. It has integration with Spring IOC, and thus it allows to use all the features of Spring.

Once the dispatcher servlet receives a request, it forwards it to handler mapping for getting an appropriate controller, and now the controller will call the correct service method and again it will send it back to the dispatcher servlet.

Again, the servlet sends the request to the view resolver for getting the required view and then it sends the response to the client browser.

Code Example to show dispatcher servlet usage:
~~~
<web-app>
 
<display-name>Software Testing Help Web Application</display-name>
 
<servlet>
<servlet-name>SoftwareTestingHelp</servlet-name>
<servlet-class>org.Springframework.web.servlet.DispatcherServlet</servlet-class>
<load-on-startup>1</load-on-startup>
</servlet>
 
<servlet-mapping>
<servlet-name>SoftwareTestingHelp</servlet-name>
<url-pattern>/</url-pattern>
</servlet-mapping>
 
</web-app>
~~~
![image](https://user-images.githubusercontent.com/100063114/158343937-c1bb7915-3b7d-423c-94ab-7ff7c25fa177.png)

# Explain Model, ModelMap and ModelAndView?
The Model interface defines a holder for model attributes. The ModelMap has a similar purpose, with the ability to pass a collection of values. It then treats those values as if they were within a Map. We should note that in Model (ModelMap) we can only store data. We put data in and return a view name.

On the other hand, with the ModelAndView, we return the object itself. We set all the required information, like the data and the view name, in the object we're returning.

# What Is ViewResolver in Spring?
The ViewResolver enables an application to render models in the browser – without tying the implementation to a specific view technology – by mapping view names to actual views.

# What Does the @ExceptionHandler Annotation Do?
The @ExceptionHandler annotation allows us to define a method that will handle the exceptions. We may use the annotation independently, but it's a far better option to use it together with the @ControllerAdvice. Thus, we can set up a global error handling mechanism. In this way, we don't need to write the code for the exception handling within every controller.

Let's take a look at the example from our article about Error Handling for REST with Spring:

@ControllerAdvice
public class RestResponseEntityExceptionHandler
  extends ResponseEntityExceptionHandler {

    @ExceptionHandler(value = { IllegalArgumentException.class,
      IllegalStateException.class })
    protected ResponseEntity<Object> handleConflict(RuntimeException ex,
      WebRequest request) {
        String bodyOfResponse = "This should be application specific";
        return handleExceptionInternal(ex, bodyOfResponse, new HttpHeaders(),
          HttpStatus.CONFLICT, request);
    }
}
We should also note that this will provide @ExceptionHandler methods to all controllers that throw IllegalArgumentException or IllegalStateException. The exceptions declared with @ExceptionHandler should match the exception used as the argument of the method. Otherwise, the exception resolving mechanism will fail at runtime.

One thing to keep in mind here is that it's possible to define more than one @ExceptionHandler for the same exception. We can't do it in the same class though since Spring would complain by throwing an exception and failing on startup.

On the other hand, if we define those in two separate classes, the application will start, but it'll use the first handler it finds, possibly the wrong one.

# Core features of Spring MVC are:

- It is capable of effectively configuring the framework and classes as beans. It also divides the functional roles and responsibilities separately.
- It allows the definition of an unlimited controller method which makes the application highly adjustable and flexible.
- It provides good customization for handler mapping, binding, view resolution, and validations.
- It helps to transfer the model by using a map. It also provides supports for velocity, JSTL, JSP, and the user can customize locale and theme resolution.
- Spring has its own tag library which makes it more flexible and supports data binding, themes, beans having life cycle up to HTTP request.

## Explain the concept of Aspect Oriented Programming?

Answer: AOP is an important part of Spring MVC Architecture. AOP is used for crosscutting concern and also for applications, validation of data, module logging, transaction management, authentication, and objects.

There are many parts of Aspect Oriented Programming. These are mentioned below:

- Aspect: Aspect is responsible for cross-cutting concerns like transaction management etc.
- Advice: It is basically an action and method that are executed and is also used for a specified join point.
- Pointcut: It is responsible for the execution of advice in terms of regular expressions.
- Joint Point: It is a point in the application for processes like exception handling, execution of the method, variable values change, etc.
- Advice Arguments: These arguments are used for passing of methods.

# What Is Spring MVC Interceptor and How to Use It?
Spring MVC Interceptors allow us to intercept a client request and process it at three places – before handling, after handling, or after completion (when the view is rendered) of a request.

The interceptor can be used for cross-cutting concerns and to avoid repetitive handler code like logging, changing globally used parameters in Spring model, etc.

For details and various implementations, take a look at Introduction to Spring MVC HandlerInterceptor article.

# What are some uses of interceptors ?	Java EE
- Authentication / Authorization
- URL forwarding
- Auditing / Logging
- Localization

# What are the advantages of Spring interceptor over Servlet Filters ?	
Ans. Spring Interceptor are Spring beans and hence they can inject other beans and can be used with other Spring frameworks concepts like AOP.

![image](https://user-images.githubusercontent.com/100063114/158345453-ee58eaed-7ad8-4e76-89aa-2175004c5bf8.png)

## Working with Interceptor

The interceptor is actually a class that either implements the HandlerInterceptor interface or extends the HandlerInterceptorAdapter, the adapter is an abstract class and does not need us to provide an implementation for all the three methods ie. preHandle(), postHandle() and afterCompletion(), which makes it easy for us to implement what we want where as HandlerInterceptor is an interface.

- preHandle() - This method is called before handling a request; it returns true, to allow the framework to send the request further to the handler method (or to the next interceptor). If the method returns false, Spring assumes that request has been handled and no further processing is needed.

- postHandle() - This hook runs when the HandlerAdapter is invoked the handler but DispatcherServlet is yet to render the view.We can use this method to add additional attributes to the ModelAndView or to determine the time taken by handler method to process a client's request.

- afterCompletion() - When a request is finished and the view is rendered, we may obtain request and response data, as well as information about exceptions.

~~~
public class LibraryInterceptor extends HandlerInterceptorAdapter {

@Override

public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception{

        
       
       String bookId = request.getParameter("id");

       if(bookId == null || Integer.parseInt(bookId)<=0){

           System.out.println("error occured");
           return false;
         }

      return true;
       

  }
    
@Override

public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView){        

      System.out.println("in postHandle can be used for model updates");
          
  
       
}

    
@Override

public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler,Exception ex){
 
       
       System.out.println("in afterCompletion");

        if (ex != null){
            ex.printStackTrace(); 

 
     }
  
}
  

}
~~~
![image](https://user-images.githubusercontent.com/100063114/158345917-5a7d3d9a-f4e2-4eb1-bc4e-29545ecc4c99.png)


