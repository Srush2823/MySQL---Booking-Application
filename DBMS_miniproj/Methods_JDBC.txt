package Cab_Booking_DBMS;

import java.sql.*;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Random;
import java.util.Calendar;


class Methods {
    static final String DB_URL = "jdbc:mysql://localhost/Cab";
    static final String USER = "root";
    static final String PASS = "MyWorkspace#23";
    Connection conn = null;
    Statement stmt = null;

    void Insert_User(String UserId, String name, String PhNo, String Home_Addr, String Work_Addr, String Email, String date) throws ClassNotFoundException, SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        stmt = conn.createStatement();

        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("connecting to the database");
            conn = DriverManager.getConnection(DB_URL, USER, PASS);


            String query = "insert into User(UserId,Name,PhNo,Home_Addr,Work_Addr,Email) values (?,?,?,?,?,?)";

            PreparedStatement prep_stmt;
            prep_stmt = conn.prepareStatement(query);
            prep_stmt.setString(1, UserId);
            prep_stmt.setString(2, name);
            prep_stmt.setString(3, PhNo);
            prep_stmt.setString(4, Home_Addr);
            prep_stmt.setString(5, Work_Addr);
            prep_stmt.setString(6, Email);

            prep_stmt.execute();
            conn.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }

    void Display_User() throws SQLException {
        String query = " select * from User ";
        int count = 0;
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery(query);
        while (rs.next()) {
            String userid = rs.getString("UserId");
            String name = rs.getString("Name");
            int phno = rs.getInt("PhNo");
            String home_addr = rs.getString("Home_Addr");
            String work_addr = rs.getString("Work_Addr");
            String email = rs.getString("Email");

            String output = "%s - %s -%d - %s - %s - %s";
            System.out.println(String.format(output, userid, name, phno, home_addr, work_addr, email));
        }
        conn.close();
    }

    void Sort_Date(String Uid) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = "select A.UserId,A.Name ,B.Date from User as A ,Trip as B where A.UserId=B.UserId and A.UserId=? order by Date";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        prep_stmt.setString(1, Uid);

        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String uid = rs.getString("UserId");
            String name = rs.getString("Name");
            String date = rs.getString("Date");

            String output = "%s - %s - %s";
            System.out.println(String.format(output, uid, name, date));
        }
        conn.close();
    }

    void Avg_Cost(String Uid) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = " select AVG(cost),Destination,UserId from Trip where UserId = ? group by Destination limit 1;";
        //String query = "select A.UserId,A.Name ,B.Date from User as A ,Trip as B where A.UserId=B.UserId and A.UserId=? order by Date";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        prep_stmt.setString(1, Uid);

        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String uid = rs.getString("AVG(cost)");
            String name = rs.getString("Destination");
            String date = rs.getString("UserId");

            String output = "%s - %s - %s";
            System.out.println(String.format(output, uid, name, date));
        }
        conn.close();
    }

    void Sort_Cost(String Uid) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = "select A.UserId,A.Name ,B.cost ,B.Date from User as A ,Trip as B where A.UserId=B.UserId and A.UserId=? order by cost;";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        prep_stmt.setString(1, Uid);

        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String uid = rs.getString("UserId");
            String name = rs.getString("Name");
            String cost = rs.getString("cost");
            String date = rs.getString("Date");

            String output = "%s - %s - %s - %s";
            System.out.println(String.format(output, uid, name, cost,date));
        }
        conn.close();
    }

    void Max_Trip(String Uid) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = "select UserId, DriverId, Location,Destination,Distance,Cost,Date from Trip where cost = (select MAX(cost) from (select cost from Trip where UserId = ?) as A)";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        prep_stmt.setString(1, Uid);

        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String uid = rs.getString("UserId");
            String did = rs.getString("DriverId");
            String loc = rs.getString("Location");
            String des = rs.getString("Destination");
            String dist = rs.getString("Distance");
            String cost = rs.getString("Cost");
            String date = rs.getString("Date");

            String output = "%s - %s - %s- %s- %s- %s- %s ";
            System.out.println(String.format(output, uid, did,loc,des,dist,cost, date));
        }
        conn.close();
    }

    void GroupBy_Dest(String Uid) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = "select count(*) as count , Destination from Trip where UserId = ? group by destination;";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        prep_stmt.setString(1, Uid);

        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String uid = rs.getString("count");
            String name = rs.getString("Destination");


            String output = "%s - %s";
            System.out.println(String.format(output, uid, name));
        }
        conn.close();
    }

    void Min_Trip(String Uid) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = "select UserId, DriverId, Location,Destination,Distance,Cost,Date from Trip where cost = (select MIN(cost) from (select cost from Trip where UserId = ?) as A)";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        prep_stmt.setString(1, Uid);

        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String uid = rs.getString("UserId");
            String did = rs.getString("DriverId");
            String loc = rs.getString("Location");
            String des = rs.getString("Destination");
            String dist = rs.getString("Distance");
            String cost = rs.getString("Cost");
            String date = rs.getString("Date");

            String output = "%s - %s - %s- %s- %s- %s- %s ";
            System.out.println(String.format(output, uid, did,loc,des,dist,cost, date));
        }
        conn.close();
    }


    public String Select_Rand() throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        String query = " SELECT DriverId FROM Driver ORDER BY RAND() LIMIT 1";
        PreparedStatement prep_stmt = conn.prepareStatement(query);
        ResultSet rs = prep_stmt.executeQuery();
        while (rs.next()) {
            String did1 = rs.getString("DriverId");
            return did1;
        }
        conn.close();
        return null;
    }

   public void InsertTrip(String UserId,String location,String destination) throws SQLException {
        conn = DriverManager.getConnection(DB_URL, USER, PASS);
        stmt = conn.createStatement();

        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("connecting to the database");
            conn = DriverManager.getConnection(DB_URL, USER, PASS);
            String driver = Select_Rand();
            System.out.println(driver);
            String query = " insert into Trip(UserId,DriverId,Location,Destination,Distance,Cost,Commission,Date) values (?,?,?,?,?,?,?,?)";
            Random r = new Random();
            int dist = r.nextInt(5,75);
            double cost = dist*10;
            double comm = cost*0.20;
            PreparedStatement prep_stmt;
            prep_stmt = conn.prepareStatement(query);

            DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy-dd-MM");

            LocalDateTime now = LocalDateTime.now();
            String date = dtf.format(now);
            System.out.println(date);

            prep_stmt.setString(1, UserId);
            prep_stmt.setString(2, driver);
            prep_stmt.setString(3, location);
            prep_stmt.setString(4, destination);
            prep_stmt.setString(5, Integer.toString(dist));
            prep_stmt.setString(6, Double.toString(cost));
            prep_stmt.setString(7, Double.toString(comm));
            prep_stmt.setString(8, date);

            prep_stmt.execute();
            //conn.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
