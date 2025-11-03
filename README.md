package com.app;

import java.io.*;
import java.sql.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class AttendanceServlet extends HttpServlet {

    protected void doPost(HttpServletRequest req, HttpServletResponse res)
            throws ServletException, IOException {

        res.setContentType("text/html");
        PrintWriter out = res.getWriter();

        String id = req.getParameter("sid");
        String date = req.getParameter("date");
        String status = req.getParameter("status");

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/college", "root", "password");

            PreparedStatement ps = con.prepareStatement(
                "INSERT INTO attendance VALUES(?,?,?)");

            ps.setInt(1, Integer.parseInt(id));
            ps.setString(2, date);
            ps.setString(3, status);

            ps.executeUpdate();
            out.println("<h3>Attendance Saved Successfully!</h3>");
            out.println("<a href='attendance.jsp'>Back</a>");

            con.close();

        } catch(Exception e) {
            out.println(e);
        }
    }
}
