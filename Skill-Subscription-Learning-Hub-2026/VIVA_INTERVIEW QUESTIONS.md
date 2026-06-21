# Viva / Interview Questions

##  Basic

- What is Spring Boot?
- Spring Boot is an extension of the Spring Framework that makes it easier and faster to build Java applications, especially web applications and microservices.
- What is MVC architecture?
- MVC (Model-View-Controller) is a software design pattern used to separate an application into three components:

Model – Manages data and business logic.
View – Displays data to the user.
Controller – Handles user requests and coordinates between Model and View.

---

##  Intermediate

- What is Service layer?
- The Service Layer is the part of an application that contains the business logic. It acts as a bridge between the Controller and the Repository (DAO) layer.
- What is Repository in Spring Data JPA?
- A Repository is a layer used to interact with the database. It performs CRUD operations (Create, Read, Update, Delete) without writing most SQL queries manually.
- Difference between GET and POST?
- GET is used to retrieve data from the server and sends parameters in the URL, whereas POST is used to send data to the server for creating or processing resources and sends data in the request body. GET is generally used for read operations, while POST is used for write operations.

---

##  Advanced (Project Based)

- How does subscription flow work?
- The subscription flow starts when a logged-in user views available skill packs and chooses a pack to subscribe to. The Controller receives the request, the Service Layer validates and processes it, the Repository saves the subscription in the database, and the user can then view the subscribed packs on the My Subscriptions page.
- How do you link User and SkillPack?
- User and SkillPack are linked through a Subscription entity. The Subscription table contains foreign keys (user_id and pack_id), creating a many-to-many relationship where one user can subscribe to multiple skill packs and one skill pack can be subscribed to by multiple users.
- Why do we use Service layer?
- We use the Service Layer to separate business logic from request handling and database access. It improves code organization, reusability, maintainability, testability, and supports transaction management. Controllers handle requests, Services implement business rules, and Repositories interact with the database.
- How does JSP get data from Controller?
- JSP gets data from the Controller through the Model object. The Controller adds data using model.addAttribute(), and the JSP accesses that data using Expression Language (${}) or JSTL tags such as <c:forEach>.
