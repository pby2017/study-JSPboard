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
8. [Board page design](https://youtu.be/pCqaGoexV5c)
 * Create bbs.jsp
 * Add table and write button
9. [Board database table](https://youtu.be/OHvWkg9Bdf0)
 * Create bean class (connect database to board class)
10. [Write page](https://youtu.be/EmbxlHakkfY)
 * Create write.jsp
 * Create writeAction.jsp


## record

## 2019 / 02 / 24 Sun
Review
* Remove attributes that I don't understand how to work
1. [Hello World](https://youtu.be/wEIBDHfoMBg)
2. [Login page](https://youtu.be/MtxFWczSFqU)
3. [Membership database](https://youtu.be/kN8xRG6UPZM)
4. [Login function](https://youtu.be/RYo3OGlRoJw)
5. [Join page](https://youtu.be/-Kbhn2TJGn4)
6. [Join function](https://youtu.be/v2mmPRLjJGw)
7. [Manage session](https://youtu.be/eJRB__ErXd4)

Create table in Board page
```html
<div class="row">
    <table class="table table-striped" style="text-align:center; border:1px solid #dddddd">
        <thead>
            <tr>
                <th style="backgroud-color: #eeeeee; text-align:center;">번호</th>
                <th style="backgroud-color: #eeeeee; text-align:center;">제목</th>
                <th style="backgroud-color: #eeeeee; text-align:center;">작성자</th>
                <th style="backgroud-color: #eeeeee; text-align:center;">작성일</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>안녕하세요</td>
                <td>홍길동</td>
                <td>2017-05-04</td>
            </tr>
        </tbody>
    </table>
    <a href="write.jsp" class="btn btn-primary pull-right">글쓰기</a>
</div>
```

Create Bbs.java
```java
(Bean / database table connect to Board Object in Java)
```

Create write.jsp
```java
<form method="post" action="writeAction.jsp">
    <table class="table table-striped"
        style="text-align: center; border: 1px solid #dddddd">
        <thead>
            <tr>
                <th colspan="2"
                    style="backgroud-color: #eeeeee; text-align: center;">게시판
                    글쓰기 양식</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><input type="text" class="form-control"
                    placeholder="글 제목" name="bbsTitle" maxlength="50"></td>
            </tr>
            <tr>
                <td><textarea class="form-control" placeholder="글 내용"
                        name="bbsContent" maxlength="2048" style="height: 350px;"></textarea></td>
            </tr>
        </tbody>
    </table>
    <input type="submit" class="btn btn-primary pull-right" value="글쓰기">
</form>
```

Create writeDAO.java for posting content
```java
public String getDate() {
    String SQL = "SELECT NOW()";
    try {
        PreparedStatement pstmt = conn.prepareStatement(SQL);
        rs = pstmt.executeQuery();
        if(rs.next()) {
            return rs.getString(1);
        }
    }catch(Exception e) {
        e.printStackTrace();
    }
    return "";
}

public int getNext() {
    String SQL = "SELECT bbsID FROM BBS ORDER BY bbsID DESC";
    try {
        PreparedStatement pstmt = conn.prepareStatement(SQL);
        rs = pstmt.executeQuery();
        if(rs.next()) {
            return rs.getInt(1) + 1;
        }
        return 1;
    }catch(Exception e) {
        e.printStackTrace();
    }
    return -1;
}

public int write(String bbsTitle, String userID, String bbsContent) {
    String SQL = "INSERT INTO BBS VALUES (?,?,?,?,?,?)";
    try {
        PreparedStatement pstmt = conn.prepareStatement(SQL);
        pstmt.setInt(1, getNext());
        pstmt.setString(2, bbsTitle);
        pstmt.setString(3, userID);
        pstmt.setString(4, getDate());
        pstmt.setString(5, bbsContent);
        pstmt.setInt(6, 1);
        return pstmt.executeUpdate();
    }catch(Exception e) {
        e.printStackTrace();
    }
    return -1;
}
```

## 2019 / 02 / 17 Sun
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

## 2019 / 02 / 13 Wed
Create User.java
```java
(Bean / database table connect to User Object in Java)
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
