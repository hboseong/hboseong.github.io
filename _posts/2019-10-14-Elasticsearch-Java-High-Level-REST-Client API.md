---
layout: post
title: "Elasticsearch Java High Level REST Client API 예제"
date: 2019-10-14 12:24:00 +0900
categories: Elasticsearch Java
tags: Elasticsearch Java
img: elasticsearch.png # Add image post (optional)  
---

```xml
import java.sql.Connection;
import java.sql.DriverManager;

public class DBConn {
    private static Connection conn = null;

    private DBConn() {
    }

    public static Connection getConnection() {
        String url = "jdbc:oracle:thin:@220.76.176.66:1521:orcl", user = "noritersand", pwd = "java301$!";
        if (conn == null) {
            try {
                Class.forName("oracle.jdbc.driver.OracleDriver");
                conn = DriverManager.getConnection(url, user, pwd);
            } catch (Exception e) {
                System.out.println(e);
            }
        }
        return conn;
    }

    public static void close() {
        if (conn != null) {
            try {
                if (!conn.isClosed())
                    conn.close();
            } catch (Exception e) {
                System.out.println(e);
            }
        }
        conn = null;
    }
}
```
