# Jdbc
It is simple jdbc program 
We have used mysql data base 
We have simple 5 steps for jdbc 
Here is code below -

import java.sql.*;
public class Jdbc {

	static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";  
	   static final String DB_URL = "jdbc:mysql://localhost:3306/dbname";
	   private static final String CREATE_TABLE_SQL="CREATE TABLE dbname.users ("
               + "UID INT NOT NULL,"
               + "NAME VARCHAR(45) NOT NULL,"
               + "DOB DATE NOT NULL,"
               + "EMAIL VARCHAR(45) NOT NULL,"
               + "PRIMARY KEY (UID))";
	   
	   private static final String CREATE_TABLE_SQL1="Insert into users values(4,'raj','1996/09/10','rajat')";

	   //  Database credentials
	   static final String USER = "root";
	   static final String PASS = "1234";
	   public static void main (String [] args){
		   
		   Connection conn = null;
		   Statement stmt = null;
		   try{
		      //STEP 2: Register JDBC driver
			   try{
		      Class.forName("com.mysql.jdbc.Driver");
		      System.out.println("driver loded");
			   }
			   catch(ClassNotFoundException e){
				   System.out.println("Hi class not found");
			   }

		      //STEP 3: Open a connection
		      System.out.println("Connecting to database...");
		      conn = DriverManager.getConnection(DB_URL,USER,PASS);

		      //STEP 4: Execute a query
		      System.out.println("Creating statement...");
		      stmt = conn.createStatement();
		   
		      //STEP 6: Clean-up environment
		     // stmt.executeUpdate(CREATE_TABLE_SQL);
		      stmt.executeUpdate(CREATE_TABLE_SQL1);
		      
		      String sql;
		      sql = "SELECT * from users";
		      ResultSet rs1 = stmt.executeQuery(sql);
		      while(rs1.next())
		      {
		    	  int empNum = rs1.getInt(1);
		    	    String lastName = rs1.getString(2);
		    	    String firstName = rs1.getString(3);
		    	    String email = rs1.getString(4);
		    	    System.out.println(empNum+lastName+firstName+email);
		      }
		     
		      
		      stmt.close();
		      conn.close();
		   }catch(SQLException se){
		      //Handle errors for JDBC
		      se.printStackTrace();
		   }catch(Exception e){
		      //Handle errors for Class.forName
		      e.printStackTrace();
		   }finally{
		      //finally block used to close resources
		      try{
		         if(stmt!=null)
		            stmt.close();
		      }catch(SQLException se2){
		      }// nothing we can do
		      try{
		         if(conn!=null)
		            conn.close();
		      }catch(SQLException se){
		         se.printStackTrace();
		      }//end finally try
		   }//end try
		   System.out.println("Goodbye!");
		   
	   }
}

