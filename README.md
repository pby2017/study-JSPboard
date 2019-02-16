# [following JSP board edu streaming by 동빈나](https://www.youtube.com/channel/UChflhu32f5EUHlY7_SetNWw)

## study curriculum
1. [Hello World](https://youtu.be/wEIBDHfoMBg)
 * Install JDK
 * Install Eclipse
2. [Login page](https://youtu.be/MtxFWczSFqU)
 * Install bootstrap 3
 * create board / menu / login page
3. [Membership database](https://youtu.be/kN8xRG6UPZM)
 * Install MySQL
 * create bean class (connect database to user class)
4. [Login function](https://youtu.be/RYo3OGlRoJw)
 * create bean
 * create action.jsp
 * connect jdbc driver in library



## record

# 2019 / 02 / 13 Wed
> Create User.java

    (Bean / database table connect to Object in Java)

> Create UserDAO.java

    database connect & login method
    PreparedStatement = protect from SQL injection

> Create loginAction.jsp

    <%@ page import="user.UserDAO" %> // using UserDAO class
    <%@ page import="java.io.PrintWriter" %> // create script tag
    <% request.setCharacterEncoding("UTF-8"); %> // get request data as UTF-8 format
    <jsp:useBean id="user" class="user.User" scope="page" /> // get data as User class format & only use in this page
    <jsp:setProperty name="user" property="userID" /> // get userID from login page input value

    <body>
        <%
            UserDAO userDAO = new UserDAO;
            int result = userDAO.login(user.getUserID(), user.getUserPassword());
            PrintWriter script = response.getWriter();
            script.println("<script>");
            script.println("location.href = 'main.jsp'");
            script.println("</script>");
        %>
    </body>
