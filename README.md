# Servlet-Jdbc
Insert the Servelet and Jdbc
/* Java File ScholarRegistration.java*/

import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;
import java.sql.*;

public class ScholarRegistration extends HttpServlet
{
	Connection con=null;
	public void init(ServletConfig config) throws ServletException
	{
		try
		{
			Class.forName("com.mysql.jdbc.Driver");
			con=DriverManager.getConnection("jdbc:mysql://localhost:3306/test","root","root");

		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
	}


	public void doPost(HttpServletRequest req,HttpServletResponse res) throws ServletException,IOException
	{
		try
		{
		PrintWriter pw=res.getWriter();
		String name=req.getParameter("name");
		String regno = req.getParameter("rgsno");
		String dept = req.getParameter("dept");
		String rtopic = req.getParameter("rt");
		String dor = req.getParameter("dt");
		String mphd = req.getParameter("mode");
		int mno = Integer.parseInt(req.getParameter("mno"));

		PreparedStatement pst=con.prepareStatement("insert into scholar values(?,?,?,?,?,?,?)");
		pst.setString(1,name);
		pst.setString(2,regno);
		pst.setString(3,dept);
		pst.setString(4,rtopic);
		pst.setString(5,dor);
		pst.setString(6,mphd);
		pst.setInt(7,mno);
		pst.executeUpdate();
		pw.println("Record Inserted Successfully");
		con.close();
		pw.close();
		pst.close();		
		}
		catch(Exception e){}

	}
	
}




/*HTML file  scholar.html*/
<!DOCTYPE html>
<html>
<head>
	<!-- Compiled and minified CSS -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/css/materialize.min.css">

    <!-- Compiled and minified JavaScript -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/js/materialize.min.js"></script>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
      <!--Import materialize.css-->
      <link type="text/css" rel="stylesheet" href="css/materialize.min.css"  media="screen,projection"/>

      <!--Let browser know website is optimized for mobile-->
      <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
	<title></title>
</head>
<body>

	<div class="row">
    	<form class="col s12" action="./Registration.me" method="post">
      		<div class="row">
      		  <div class="input-field col s6">
        		  <input id="name" type="text" class="validate" name="name">
       		      <label for="name">Name of the PhD Scholar:-</label>
        	  </div>	
            </div>

			
            <div class="row">
      		  <div class="input-field col s6">
        		  <input id="rgs" name="rgsno" type="text" class="validate">
       		      <label for="rgs">Registration No:-</label>
        	  </div>	
            </div>


            <div class="row">
      		  <div class="input-field col s6">
        		  <input id="dept" name="dept" type="text" class="validate">
       		      <label for="dept">Department:-</label>
        	  </div>	
            </div>


            <div class="row">
      		  <div class="input-field col s6">
        		  <input id="rt" name="rt" type="text" class="validate">
       		      <label for="rt">Reasearch Topic:-</label>
        	  </div>	
            </div>


            <div class="row">
      		  <div class="input-field col s6">
        		  <input id="dt" type="date" class="validate" name="dt">
       		      <label for="dt">Date of Registration:-</label>
        	  </div>	
            </div>


            <div class="row">
      		  <div class="input-field col s6">
        		  <input id="mode" type="text" class="validate" name="mode">
       		      <label for="mode">Mode of the PhD(part/full) Time:-</label>
        	  </div>	
            </div>


            <div class="row">
      		  <div class="input-field col s6">
        		  <input id="mno" name="mno" type="text" class="validate">
       		      <label for="name">Mobile No:-</label>
        	  </div>	
            </div>


			<div class="row">
      		  <div class="input-field col s6">
        		  <input name="submit" type="submit" class="validate">
        	  </div>	
            </div>

        </form>
    </div>
</body>
</html>


/*XML file web.xml*/

<web-app>  
  
<servlet>  
<servlet-name>shubham</servlet-name>  
<servlet-class>TeacherRegistration</servlet-class>  
</servlet>  
  
<servlet-mapping>  
<servlet-name>shubham</servlet-name>  
<url-pattern>/Registration.me</url-pattern>  
</servlet-mapping>  
  
</web-app>  
