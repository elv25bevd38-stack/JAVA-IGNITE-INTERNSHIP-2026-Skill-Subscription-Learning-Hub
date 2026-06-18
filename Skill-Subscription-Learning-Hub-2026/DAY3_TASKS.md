# DAY 3 — Frontend Integration (JSP)

##  Goal
Connect backend with UI

---

##  TASK 1: JSP Pages

Create:

- register.jsp
- login.jsp
- packs.jsp
- add-pack.jsp
- subscriptions.jsp
<%@ page language="java" contentType="text/html;charset=UTF-8" %>

<html>
<head>
    <title>Register</title>
</head>
<body>

<h2>User Registration</h2>

<form action="register" method="post">
    Name:
    <input type="text" name="name" required><br><br>

    Email:
    <input type="email" name="email" required><br><br>

    Password:
    <input type="password" name="password" required><br><br>

    <input type="submit" value="Register">
</form>

<a href="login.jsp">Login</a>

</body>
</html>
<%@ page language="java" contentType="text/html;charset=UTF-8" %>

<html>
<head>
    <title>Login</title>
</head>
<body>

<h2>User Login</h2>

<form action="login" method="post">

    Email:
    <input type="email" name="email" required><br><br>

    Password:
    <input type="password" name="password" required><br><br>

    <input type="submit" value="Login">

</form>

<a href="register.jsp">Register</a>

</body>
</html> 
<%@ page language="java" contentType="text/html;charset=UTF-8" %>

<html>
<head>
    <title>Skill Packs</title>
</head>
<body>

<h2>Available Skill Packs</h2>

<table border="1">
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Price</th>
    </tr>

    <%
        List<SkillPack> packs =
                (List<SkillPack>) request.getAttribute("packs");

        if(packs != null){
            for(SkillPack p : packs){
    %>

    <tr>
        <td><%= p.getId() %></td>
        <td><%= p.getName() %></td>
        <td><%= p.getPrice() %></td>
    </tr>

    <%
            }
        }
    %>

</table>

<br>
<a href="add-pack.jsp">Add New Pack</a>

</body>
</html> 
<%@ page language="java" contentType="text/html;charset=UTF-8" %>

<html>
<head>
    <title>Add Skill Pack</title>
</head>
<body>

<h2>Add Skill Pack</h2>

<form action="addPack" method="post">

    Pack Name:
    <input type="text" name="name" required><br><br>

    Description:
    <input type="text" name="description" required><br><br>

    Price:
    <input type="number" step="0.01" name="price" required><br><br>

    <input type="submit" value="Add Pack">

</form>

</body>
</html> 
<%@ page language="java" contentType="text/html;charset=UTF-8" %>

<html>
<head>
    <title>Subscriptions</title>
</head>
<body>

<h2>My Subscriptions</h2>

<table border="1">

<tr>
    <th>ID</th>
    <th>Skill Pack</th>
    <th>Start Date</th>
    <th>End Date</th>
    <th>Status</th>
</tr>

<%
    List<Subscription> subscriptions =
            (List<Subscription>)request.getAttribute("subscriptions");

    if(subscriptions != null){
        for(Subscription s : subscriptions){
%>

<tr>
    <td><%= s.getId() %></td>
    <td><%= s.getSkillPack().getName() %></td>
    <td><%= s.getStartDate() %></td>
    <td><%= s.getEndDate() %></td>
    <td><%= s.getStatus() %></td>
</tr>

<%
        }
    }
%>

</table>

</body>
</html>
---

##  TASK 2: Display Data

Use JSTL:
- Loop skill packs
- Display subscriptions
- Show user data
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<html>
<head>
    <title>Skill Packs</title>
</head>
<body>

<h2>Available Skill Packs</h2>

<table border="1">
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Description</th>
        <th>Price</th>
    </tr>

    <c:forEach var="pack" items="${packs}">
        <tr>
            <td>${pack.id}</td>
            <td>${pack.name}</td>
            <td>${pack.description}</td>
            <td>${pack.price}</td>
        </tr>
    </c:forEach>

</table>

</body>
</html>
request.setAttribute("packs", skillPackService.getAllPacks());
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<html>
<head>
    <title>Subscriptions</title>
</head>
<body>

<h2>My Subscriptions</h2>

<table border="1">

<tr>
    <th>ID</th>
    <th>Skill Pack</th>
    <th>Start Date</th>
    <th>End Date</th>
    <th>Status</th>
</tr>

<c:forEach var="sub" items="${subscriptions}">
    <tr>
        <td>${sub.id}</td>
        <td>${sub.skillPack.name}</td>
        <td>${sub.startDate}</td>
        <td>${sub.endDate}</td>
        <td>${sub.status}</td>
    </tr>
</c:forEach>

</table>

</body>
</html>
request.setAttribute("subscriptions",
                     subscriptionService.getUserSubscriptions(userId));

           <%@ page contentType="text/html;charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<html>
<head>
    <title>User Profile</title>
</head>
<body>

<h2>User Details</h2>

<p><b>ID:</b> ${user.id}</p>
<p><b>Name:</b> ${user.name}</p>
<p><b>Email:</b> ${user.email}</p>

</body>
</html>          
<c:choose>
    <c:when test="${sub.status == 'ACTIVE'}">
        Active
    </c:when>

    <c:otherwise>
        Expired
    </c:otherwise>
</c:choose>
<c:if test="${empty packs}">
    <p>No Skill Packs Available</p>
</c:if>

<dependency>
    <groupId>jakarta.servlet.jsp.jstl</groupId>
    <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
    <version>3.0.0</version>
</dependency>

<dependency>
    <groupId>org.glassfish.web</groupId>
    <artifactId>jakarta.servlet.jsp.jstl</artifactId>
    <version>3.0.1</version>
</dependency>---

##  TASK 3: Navigation Flow

Ensure:

- Login → Packs page
- Subscribe → My Subscriptions
- Logout → Login page

---

##  Focus Areas

- JSP binding with Model
- Controller → View mapping
- UI flow understanding
- @Controller
public class LoginController {

    @Autowired
    private UserService userService;

    @PostMapping("/login")
    public String login(
            @RequestParam String email,
            @RequestParam String password,
            HttpSession session,
            Model model) {

        User user = userService.login(email, password);

        if (user == null) {
            model.addAttribute("error",
                    "Invalid Email or Password");
            return "login";
        }

        session.setAttribute("user", user);

        return "redirect:/packs";
    }

} 
@Controller
public class SkillPackController {

    @Autowired
    private SkillPackService skillPackService;

    @GetMapping("/packs")
    public String viewPacks(Model model) {

        model.addAttribute(
                "packs",
                skillPackService.getAllPacks());

        return "packs";
    }
} 
<h2>Available Skill Packs</h2>

<c:forEach var="pack" items="${packs}">
    <p>
        ${pack.name}
        - ₹${pack.price}

        <a href="subscribe?packId=${pack.id}">
            Subscribe
        </a>
    </p>
</c:forEach>

<a href="logout">Logout</a> 
@Controller
public class SubscriptionController {

    @Autowired
    private SubscriptionService subscriptionService;

    @GetMapping("/subscribe")
    public String subscribe(
            @RequestParam int packId,
            HttpSession session) {

        User user =
                (User) session.getAttribute("user");

        subscriptionService.subscribe(
                user.getId(),
                packId);

        return "redirect:/subscriptions";
    }
} 
@GetMapping("/subscriptions")
public String mySubscriptions(
        HttpSession session,
        Model model) {

    User user =
            (User) session.getAttribute("user");

    model.addAttribute(
            "subscriptions",
            subscriptionService
                    .getUserSubscriptions(user.getId()));

    return "subscriptions";
} 
<h2>My Subscriptions</h2>

<table border="1">

<tr>
    <th>Pack</th>
    <th>Status</th>
    <th>Start Date</th>
    <th>End Date</th>
</tr>

<c:forEach var="sub"
           items="${subscriptions}">

    <tr>
        <td>${sub.skillPack.name}</td>
        <td>${sub.status}</td>
        <td>${sub.startDate}</td>
        <td>${sub.endDate}</td>
    </tr>

</c:forEach>

</table>

<a href="packs">Back to Packs</a>
<a href="logout">Logout</a> 
@GetMapping("/logout")
public String logout(HttpSession session) {

    session.invalidate();

    return "redirect:/login";
} 
Welcome, ${sessionScope.user.name}

<hr>

<a href="subscriptions">
    My Subscriptions
</a>
|
<a href="logout">
    Logout
</a>
