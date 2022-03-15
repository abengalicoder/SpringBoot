### What are some essential features of Spring Security?
Some essential features of Spring Security include: 

- Supports authentication and authorization in a flexible and comprehensive manner.
- Detection and prevention of attacks including session fixation, clickjacking, cross-site request forgery, etc.
- Integrate with Servlet API.
- Offers optional integration with Spring Web MVC (Model-View-Controller).
- Java Authentication and Authorization Service (JAAS) is used for authentication purposes.
- Allows Single Sign-On so that users can access multiple applications with just one account (username and password)

### How is Security mechanism implemented using Spring
Spring Security is a powerful and highly customizable authentication and access-control framework. It is the de-facto standard for securing Spring-based applications. Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements.

**Spring makes use of the DelegatingFilterProxy for implementing security mechanisms.** It is a Proxy for standard Servlet Filter, delegating to a Spring-managed bean that implements the Filter interface. Its the starting point in the springSecurityFilterChain which instantiates the Spring Security filters according to the Spring configuration
Some of the features of Spring Security are
 - Comprehensive and extensible support for both Authentication and Authorization
 - Protection against attacks like session fixation, clickjacking, cross site request forgery, etc
 - Servlet API integration Optional integration with Spring Web MVC

### What is Spring security authentication and authorization?
- Authentication: This refers to the process of verifying the identity of the user, using the credentials provided when accessing certain restricted resources. Two steps are involved in authenticating a user, namely identification and verification. An example is logging into a website with a username and a password. This is like answering the question Who are you?  
- Authorization: It is the ability to determine a user's authority to perform an action or to view data, assuming they have successfully logged in. This ensures that users can only access the parts of a resource that they are authorized to access. It could be thought of as an answer to the question Can a user do/read this?
![image](https://user-images.githubusercontent.com/100063114/158349355-6414d070-fd43-4641-bfac-439314b888c1.png)

### Explain SecurityContext and SecurityContext Holder in Spring security.
There are two fundamental classes of Spring Security: SecurityContext and SecurityContextHolder.  

- SecurityContext: In this, information/data about the currently authenticated user (also known as the principal) is stored. So, in order to obtain a username or any other information about the user, you must first obtain the SecurityContext.
- SecurityContextHolder: Retrieving the currently authenticated principal is easiest via a static call to the SecurityContextHolder. As a helper class, it provides access to the security context. By default, it uses a ThreadLocal object to store SecurityContext, so SecurityContext is always accessible to methods in the same thread of execution, even if SecurityContext isn't passed around

### Explain spring security OAuth2.
A simple authorization framework, OAuth 2.0, permits client applications to access protected resources via an authorization server. Using it, a client application (third party) can gain limited access to an HTTP service on behalf of the resource owner or on its own behalf. 

there are four roles in oauth2.0
- Resource Owner/User: The owner of a resource, i.e., the individual who holds the rights to that resource.
- Client: The application requests an access token (represents a user's permission for the client to access their data/resources), then accesses the protected resource server after receiving the access token.
- Authorization Server: After successfully authenticating the resource owner and obtaining authorization, the server issues access tokens to the client.
- Resource Server: It provides access to requested resources. Initially, it validates the access tokens, then it provides authorization
![image](https://user-images.githubusercontent.com/100063114/158349976-fcf2c425-8f61-4363-9610-97f3af126ba8.png)

# What do you mean by OAuth2 Authorization code grant type?
The term "grant type" in OAuth 2.0 refers to the way an application gets an access token. The authorization code flow is one of several types of grants defined by OAuth 2.0. This grant is used by both web applications and native applications to obtain an access token after a user authorizes the application. As opposed to most other grant types, it requires the application to first launch a browser to begin the process/flow. The process involves the following steps:  

- The application opens a browser to direct the user to an OAuth server.
- Upon seeing the authorization prompt, the user approves the application's request.
- Upon approval, the user is redirected back to the application with an authorization code in the query string.
- Application exchange authorization codes for access tokens

### What is PasswordEncoder?
Password encoding is provided by Spring Security using the PasswordEncoder interface. This interface defines two methods:  

encode(): It converts a plain password into an encoded form.
matches(): It compares an encoded password from the database with a plain password (input by the user) that's been encoded using the same salting and hashing algorithm as the encoded password

### What is JWT?
JWT (JSON Web Tokens) are tokens that are generated by a server upon user authentication in a web application and are then sent to the client (normally a browser). As a result, these tokens are sent on every HTTP request, allowing the server to verify or authenticate the user's identity. This method is used for authorizing transactions or requests between client and server. The use of JWT does not intend to hide data, but rather ensure its authenticity. JWTs are signed and encoded, instead of encrypted. A cryptographic algorithm is used to digitally sign JWTs in order to ensure that they cannot be altered after they are issued. Information contained in the token is signed by the server's private key in order to ensure integrity. 
![image](https://user-images.githubusercontent.com/100063114/158350645-e9925f0b-d01c-4636-b9f3-38ea52ce0f4e.png)

### Name some predefined filters used in spring security and write their functions.
Filter chains in Spring Security are very complex and flexible. They use services such as UserDetailsService and AuthenticationManager to accomplish their tasks. It is also important to consider their orders since you might want to verify their authenticity before authorizing them. A few of the important security filters from Spring's filter chain are listed below in the order they occur: 

- SecurityContextPersistenceFilter: Stores the SecurityContext contents between HTTP requests. It also clears SecurityContextHolder when a request is finished.
- ConcurrentSessionFilter: It is responsible for handling concurrent sessions. Its purpose is to refresh the last modified time of the request's session and to ensure the session hasn't expired.
- UsernamePasswordAuthenticationFilter: It's the most popular authentication filter and is the one that's most often customized.
- ExceptionTranslationFilter: This filter resides above FilterSecurityInterceptor in the security filter stack. Although it doesn't perform actual security enforcement, it handles exceptions thrown by the security interceptors and returns valid and suitable HTTP responses.
- FilterSecurityInterceptor: It is responsible for securing HTTP resources (web URIs), and raising or throwing authentication and authorization exceptions when access is denied

### What do you mean by principal in Spring security?
The principal is actually the currently logged in user that is using the application. Information/data about the principal (currently authenticated user) is stored in the SecurityContext of the application. As a helper class, SecurityContextHolder provides access to the security context. By default, it uses a ThreadLocal object to store SecurityContext, so SecurityContext is always accessible to methods in the same thread of execution, even if SecurityContext isn't passed around explicitly



