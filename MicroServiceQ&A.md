
### What do you mean by Microservice?
Microservices, also known as Microservices Architecture, is basically an SDLC approach in which large applications are built as a collection of small functional modules. It is one of the most widely adopted architectural concepts within software development. In addition to helping in easy maintenance, this architecture also makes development faster. Additionally, microservices are also a big asset for the latest methods of software development such as DevOps and Agile. Furthermore, it helps deliver large, complex applications promptly, frequently, and reliably. Applications are modeled as collections of services, which are: 

- Maintainable and testable
- Loosely coupled
- Independently deployable
- Designed or organized around business capabilities
- Managed by a small team
- ![image](https://user-images.githubusercontent.com/100063114/158346321-3ee122fe-a425-48c9-94fb-c5e1ae66c188.png)

## 1. Write main features of Microservices.
- Decoupling: Within a system, services are largely decoupled. The application as a whole can therefore be easily constructed, altered, and scalable
- Componentization: Microservices are viewed as independent components that can easily be exchanged or upgraded
- Business Capabilities: Microservices are relatively simple and only focus on one service
- Team autonomy: Each developer works independently of each other, allowing for a faster project timeline
- Continuous Delivery: Enables frequent software releases through systematic automation of software development, testing, and approval
- Responsibility: Microservices are not focused on applications as projects. Rather, they see applications as products they are responsible for
- Decentralized Governance: Choosing the right tool according to the job is the goal. Developers can choose the best tools to solve their problems
- Agility: Microservices facilitate agile development. It is possible to create new features quickly and discard them again at any time
![image](https://user-images.githubusercontent.com/100063114/158346522-329c3a23-7dda-442e-895f-1e26d6afd81d.png)

### Write main components of Microservices.
Some of the main components of microservices include: 

- Containers, Clustering, and Orchestration 
- IaC [Infrastructure as Code Conception] 
- Cloud Infrastructure 
- API Gateway 
- Enterprise Service Bus 
- Service Delivery 
### What are the benefits and drawbacks of Microservices?
Benefits: 

- Self-contained, and independent deployment module. 
- Independently managed services.   
- In order to improve performance, the demand service can be deployed on multiple servers.   
- It is easier to test and has fewer dependencies.  
- A greater degree of scalability and agility.   
- Simplicity in debugging & maintenance.  
- Better communication between developers and business users.   
- Development teams of a smaller size.
Drawbacks: 

- Due to the complexity of the architecture, testing and monitoring are more difficult.  
- Lacks the proper corporate culture for it to work.   
- Pre-planning is essential.  
- Complex development.  
- Requires a cultural shift.  
- Expensive compared to monoliths.   
- Security implications. 
- Maintaining the network is more difficult.

### Explain the working of Microservice Architecture.
Microservice architectures consist of the following components: 

- Clients: Different users send requests from various devices. 
- Identity Provider: Validate a user's or client's identity and issue security tokens. 
- API Gateway: Handles the requests from clients. 
- Static Content: Contains all of the system's content. 
- Management: Services are balanced on nodes and failures are identified. 
- Service Discovery: A guide to discovering the routes of communication between microservices. 
- Content Delivery Network: Includes distributed network of proxy servers and their data centers. 
- Remote Service: Provides remote access to data or information that resides on networked computers and devices
![image](https://user-images.githubusercontent.com/100063114/158347098-d5f19041-c1d4-4d51-9b3f-ddce5043368d.png)

### Explain spring cloud and spring boot.
- Spring Cloud: In Microservices, the Spring cloud is a system that integrates with external systems. This is a short-lived framework designed to build applications quickly. It contributes significantly to microservice architecture due to its association with finite amounts of data processing. Some of the features of spring cloud are shown below:
![image](https://user-images.githubusercontent.com/100063114/158347290-a4084fb7-d3eb-43b5-bbe4-eac911274f84.png)

- Spring Boot: Spring Boot is an open-sourced, Java-based framework that provides its developers with a platform on which they can create stand-alone, production-grade Spring applications. In addition to reducing development time and increasing productivity, it is easily understood.
![image](https://user-images.githubusercontent.com/100063114/158347377-bc5a1101-cd2f-4182-b97f-960e12551dc9.png)

## What issues are generally solved by spring clouds?
The following problems can be solved with spring cloud:   

- Complicated issues caused by distributed systems: This includes network issues, latency problems, bandwidth problems, and security issues. 
- Service Discovery issues: Service discovery allows processes and services to communicate and locate each other within a cluster. 
- Redundancy issues: Distributed systems can often have redundancy issues. 
- Load balancing issues: Optimize the distribution of workloads among multiple computing resources, including computer clusters, central processing units, and network links. 
- Reduces performance issues: Reduces performance issues caused by various operational overheads.

# Write the fundamental characteristics of Microservice Design.
Based on Business Capabilities: Services are divided and organized around business capabilities. 
- Products not projects: A product should belong to the team that handles it.  
- Essential messaging frameworks: Rely on functional messaging frameworks: Eliminate centralized service buses by embracing the concept of decentralization.  
- Decentralized Governance: The development teams are accountable for all aspects of the software they produce.  
- Decentralized data management: Microservices allow each service to manage its data separately.  
- Automated infrastructure: These systems are complete and can be deployed independently.   
- Design for failure: Increase the tolerance for failure of services by focusing on continuous monitoring of the applications. 

### What are the challenges that one has to face while using Microservices?
The challenges that one has to face while using microservices can be both functional and technical as given below: 

Functional Challenges:

- Require heavy infrastructure setup. 
- Need Heavy investment. 
- Require excessive planning to handle or manage operations overhead.

Technical Challenges:

- Microservices are always interdependent. Therefore, they must communicate with each other.   
- It is a heavily involved model because it is a distributed system.   
- You need to be prepared for operations overhead if you are using Microservice architecture.   
- To support heterogeneously distributed microservices, you need skilled professionals.    
- It is difficult to automate because of the number of smaller components. For that reason, each component must be built, deployed, and monitored separately.   
- It is difficult to manage configurations across different environments for all components. 
- Challenges associated with deployment, debugging, and testing
