# [following JSP board edu streaming by 동빈나](https://www.youtube.com/channel/UChflhu32f5EUHlY7_SetNWw)

## study curriculum
1. [Hello World](https://youtu.be/wEIBDHfoMBg)
 * Install JDK
 * Install Eclipse
2. [Login page](https://youtu.be/MtxFWczSFqU)
 * Install bootstrap 3
 * Create board / menu / login page
3. [Membership database](https://youtu.be/kN8xRG6UPZM)
 * Install MySQL
 * Create bean class (connect database to user class)
4. [Login function](https://youtu.be/RYo3OGlRoJw)
 * Create bean
 * Create loginAction.jsp
 * Connect jdbc driver in library
5. [Join page](https://youtu.be/-Kbhn2TJGn4)
 * Create join page
6. [Join function](https://youtu.be/v2mmPRLjJGw)
 * Create bean
 * Create joinAction.jsp
7. [Manage session](https://youtu.be/eJRB__ErXd4)
 * HttpSession session
 * Create logoutAction.jsp
 * Move from index.jsp to main.jsp

## record

# 2019 / 02 / 24 Sun
Review
* [Hello World](https://youtu.be/wEIBDHfoMBg)
* [Login page ~10:10](https://youtu.be/MtxFWczSFqU?t=610)

# 2019 / 02 / 17 Sun
Create join.jsp
```html
<div class="form-group" style="align:center;">
    <div class="btn-group" data-toggle="buttons">
        <label class="btn btn-primary active">
            <input type="radio" name="userGender" autocomplete="off" value="남자" checked>남자
        </label>
        <label class="btn btn-primary">
            <input type="radio" name="userGender" autocomplete="off" value="여자" checked>여자
        </label>
    </div>
</div>
```

Create joinAction.jsp
```java
<jsp:setProperty name="user" property="userName" />
<jsp:setProperty name="user" property="userGender" />
<jsp:setProperty name="user" property="userEmail" />

int result = userDAO.join(user);
```

Add session
```java
String userID = null;
if(session.getAttribute("userID") != null){
    userID = (String) session.getAttribute("userID");
}
```

Add session true / false situation
```java
<%
    if(userID == null){ 
%>
body~~
<%
    }
%>
```

Create logoutAction.jsp
```java
<%
    session.invalidate();
%>
```

# 2019 / 02 / 13 Wed
Create User.java
```java
(Bean / database table connect to Object in Java)
```

Create UserDAO.java
```java
database connect & login method
PreparedStatement = protect from SQL injection
```

Create loginAction.jsp
```java
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
```
