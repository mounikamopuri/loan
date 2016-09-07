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
