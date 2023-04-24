---
title: Microserices - Not a Binary Choice
weight: 1
authors:
  - sathishk
authorimage: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSOd256TcC6vcaQ99TYzoP0pBbch9_Q-bbrmw&usqp=CAU'
---

### Chapter 1: The Great Debate: Monoliths vs. Microservices
As software engineers, we face numerous challenges on a daily basis. Perhaps your team is struggling to stay productive, your application isn't scalable enough, or your response times are sluggish. Or maybe you're simply having a hard time acing those job interviews. It can be overwhelming to tackle each problem individually, which is why many software gurus are promoting a single solution for all of these issues: microservices.

But what exactly are microservices, and why is there so much pressure in the industry to adopt them? For starters, it seems like monoliths - the traditional way of building software - have become outdated and old-fashioned. Yet at the same time, many experts are now recommending a hybrid approach known as modular monoliths.

Before we dive into the technical details, let's take a step back and explore the basics. What are monoliths and microservices, and how are they connected? By understanding the fundamental principles behind these two architectures, we can better appreciate the benefits and drawbacks of each. So let's get started!

### Chapter 2: A Cautionary Tale

Meet Mr. Developer, a software engineer who was running a monolithic REST API application on a single Tomcat instance connected to MySQL. He had heard a lot of buzz about microservices and saw his competitors successfully adopting this architecture, so he decided to follow suit. Mr. Developer split his monolith into two microservices, each with its own database: MySQL and MongoDB.

However, Mr. Developer quickly realized that the transition was not as smooth as he expected. He encountered a few problems that he hadn't anticipated:

1. **Cloud cost:** What was previously running on just two nodes (Tomcat and MySQL) now required at least six nodes, including an API gateway node, two services nodes, a MySQL server, a MongoDB server, and additional nodes for distributed logging and tracing.
2. **Performance:** Each REST call now needed to be encoded and decoded twice, resulting in additional processing time that slowed down the system.
3. **Complexity:** As he separated the services, his team also got split. Additionally, Mr. Developer needed to acquire new skills like MongoDB, distributed logging, and tracing, which resulted in additional complexity.
4. **Lack of Standard** Due to the lack of standard he has to rework on things that was not even in his coontrol. (E.g Open Feign Deprecation, Outdated Netflix Libraries)

Mr. Developer found himself dealing with complexity, increased costs, and lower performing software. He couldn't help but wonder what had gone wrong in his transition from monolith to microservices.

### Chapter 3: Monoliths and Microservices as Families

#### The Joint Family: Monoliths
In the context of software engineering, a monolith can be thought of as a joint family - a large and tightly-knit group of software components that work together to achieve a common goal.

Just like in a joint family, all the services in a monolith are closely connected to one another, sharing resources and relying on each other for support. While this can lead to a strong sense of camaraderie and mutual aid, it can also result in conflicts and inefficiencies if not managed properly.

#### The Nuclear Family: Microservices
On the other hand, microservices can be thought of as a nuclear family - a small and self-sufficient group of software components that work independently, but still share a common goal.

Unlike a joint family, where resources are shared and communication is constant, each microservice operates in its own isolated environment. This allows for greater flexibility and autonomy, but can also lead to isolation and fragmentation if not properly managed.

#### Choosing the Right Family: Monoliths vs. Microservices
It's important to note that the choice between monoliths and microservices should be driven by the specific requirements of your software, not external factors like trends or what others are doing.

If you choose to go with a monolith simply because it's the "traditional" approach, or because other companies in your industry are using it, you may end up paying a heavy price in terms of scalability, maintainability, and overall performance.

Similarly, if you choose microservices without carefully considering the complexity of your system or the potential communication overhead between services, you may find yourself struggling to manage a fragmented and inefficient architecture.

In short, the key to making the right choice is to carefully evaluate your software requirements and choose the architecture that best aligns with those needs. This may require some trial and error, but in the long run it will pay off in terms of better performance, greater scalability, and easier maintenance.

### Chapter 4: Microservices: Deconstructing the Vada Pav

Let's take a closer look at microservices by comparing it to a popular Indian street food called Vada Pav. Just like the Vada Pav, microservices consist of several individual components that work together to create a cohesive end product.

![Vapav](/images/vadapav.png)

1. The Bun serves as the platform to hold everything together, and it can be purchased from different vendors like Master Bakery or KR Bakery.
2. The Masala Topping serves as the foundation layer and adds flavor to the dish.
3. The Bonda and Chutney are made in-house by the Vadapav maker. Making the Bonda requires expertise in frying and the use of a frying pan, while making the Chutney requires knowledge of grinding and the use of a mixer.

Similarly, Java-based microservices also have three main components:

1. The Java Virtual Machine (JVM) serves as the platform and can be provided by different vendors like Oracle, Azul, or OpenJDK.
2. Frameworks and tools, like Spring Boot or Quarkus, serve as the foundation layer and provide structure to the microservices.
3. Building the Bonda Service may require expertise in Java, while building the Chutney Service may require knowledge of Python. Additionally, the tools used to build each service may differ as well. The Bonda Service may be built using Spring Boot, while the Chutney Service may be built using Django.

In an ideal world of service-oriented development, these four components (JVM, frameworks and tools, our own services, and external services) should be flexible enough to be replaced, just like how one can replace the bun or masala topping in a Vada Pav.

### Conclusion

1. Monolith is not a bad approach if it works properly. In some cases, a monolithic architecture can be sufficient to meet the needs of the application and its users.
2. It's generally not advisable to start a new project using a microservices architecture. This approach adds complexity and can be challenging to manage, especially for smaller teams.
3. It's better to develop the application as a monolith first and then consider deploying it as microservices if necessary. This approach allows for easier testing, debugging, and development, while also allowing for easier deployment and scaling in the future.