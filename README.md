ADMIN.HTML
--------------
<html>
<head>
<meta http-equiv="Content-Language" content="en-us">
<meta http-equiv="Content-Type" content="text/html; charset=windows-1252">
</head><title>Admin</title>
<style>
thead th { text-align:center; background:blue; color:white; width:1850px; height:20px}</style>
<body>
<p>
<table>
<thead>
<tr>
<th><font size="50">Loan Management</font></th>
</tr>
</thead>
</table></p><br><br><br>
<form action="Admin" method="post">
<div style="text-align:center">
<h3 style="color:blue;">Admin</h3>
 &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;Username&nbsp;&nbsp;:
  <input type="text" name="username"><br><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Password&nbsp;&nbsp;:
  <input type="password" name="password"><br><br>
 &nbsp; <br><br>
 <input type="submit" value="Login"/>
 
 ADMIN.JAVA
 ----------------
package com.loan;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class Admin
 */
@WebServlet("/Admin")
public class Admin extends HttpServlet {
	private static final long serialVersionUID = 1L;
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
	response.setContentType("text/html;charset=UTF-8");
    PrintWriter out = response.getWriter();
    
    String username = request.getParameter("username");
    String password= request.getParameter("password");
    
    if(username.equals("admin")&&(Validate.checkUser(username, password)))      
    {
        RequestDispatcher rs = request.getRequestDispatcher("home.html");
        rs.forward(request, response);
    }
     else
    {
    	out.println("username or password is incorrect");
       RequestDispatcher rs = request.getRequestDispatcher("admin.html");
       rs.include(request, response);
    }
}  
}
VALIDATE.JAVA
----------------

package com.loan;

import java.sql.*;

public class Validate
 {
     public static boolean checkUser(String admin,String password) 
     {
      boolean st =true;
      
      try{

	 //loading drivers for mysql
         Class.forName("com.mysql.jdbc.Driver");
     //creating connection with the database 
         Connection con=DriverManager.getConnection
                        ("jdbc:mysql://localhost:3306/loan_mgt","root","myroot");
         PreparedStatement ps =con.prepareStatement
                             ("select * from admin where username=? and password=?");
         ps.setString(1, admin);
         ps.setString(2, password);
         ResultSet rs =ps.executeQuery();
         st = rs.next();
        
      }catch(Exception e)
      {
          e.printStackTrace();
      }
         return st;                 
  }

}
--------------------------------Admin end---------------------------------------
-------------------HOME PAGE------------
HOME.HTML
<!DOCTYPE html>
<html>
<head>
<style>
body {margin:0;}
ul.topnav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

ul.topnav li {float: left;}

ul.topnav li a {
  display: inline-block;
  color: #f2f2f2;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  transition: 0.3s;
  font-size: 17px;
}

ul.topnav li a:hover {background-color: #555;}

ul.topnav li.icon {display: none;}

@media screen and (max-width:680px) {
  ul.topnav li:not(:first-child) {display: none;}
  ul.topnav li.icon {
    float: right;
    display: inline-block;
  }
}

@media screen and (max-width:680px) {
  ul.topnav.responsive {position: relative;}
  ul.topnav.responsive li.icon {
    position: absolute;
    right: 0;
    top: 0;
  }
  ul.topnav.responsive li {
    float: none;
    display: inline;
  }
  ul.topnav.responsive li a {
    display: block;
    text-align: left;
  }
}
!--Drop Menu Bar--!
#primary_nav_wrap
{
	margin-top:15px
}

#primary_nav_wrap ul
{
	list-style:none;
	position:relative;
	float:left;
	margin:0;
	padding:0
}

#primary_nav_wrap ul a
{
	display:block;
	color:#333;
	text-decoration:none;
	font-weight:700;
	font-size:12px;
	line-height:32px;
	padding:0 15px;
	font-family:"HelveticaNeue","Helvetica Neue",Helvetica,Arial,sans-serif
}

#primary_nav_wrap ul li
{
	position:relative;
	float:left;
	margin:0;
	padding:0
}

#primary_nav_wrap ul li.current-menu-item
{
	background:#ddd
}

#primary_nav_wrap ul li:hover
{
	background:#f6f6f6
}

#primary_nav_wrap ul ul
{
	display:none;
	position:absolute;
	top:100%;
	left:0;
	background:#fff;
	padding:0
}

#primary_nav_wrap ul ul li
{
	float:none;
	width:200px
}

#primary_nav_wrap ul ul a
{
	line-height:120%;
	padding:10px 15px
}

#primary_nav_wrap ul ul ul
{
	top:0;
	left:100%
}

#primary_nav_wrap ul li:hover > ul
{
	display:block
}
</style>
</head>
<style>
thead th { text-align:center; background:blue; color:white; width:1850px; height:20px}</style>
<body background="images.png">
<table>
<thead>
<tr>
<th><font size="50" align="center">Loan Management</font></th>
</tr>
</thead>
</table>
<ul class="topnav" id="myTopnav">
  <li><a class="active" href="home.html">HOME</a></li>
  <li><a href="#news">CUSTOMER DETAILS</a></li>
  <li><a href="#contact">LOAN DETAILS</a></li>
  <li><a href="#about">EMI CALCULATIONS</a></li>
  <li><a href="#about">RECEIVE PAYMENT</a></li>
  <li><a href="menulist.html">MENU LIST</a></li>
  
  <li class="icon">
    <a href="javascript:void(0);" style="font-size:15px;" onclick="myFunction()">☰</a>
  </li>
</ul>

<div style="padding-left:16px">
  <h2></h2>
  <p></p>
</div>

<script>
function myFunction() {
    var x = document.getElementById("myTopnav");
    if (x.className === "topnav") {
        x.className += " responsive";
    } else {
        x.className = "topnav";
    }
}
</script>
</body>
</html>


