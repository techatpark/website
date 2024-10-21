---
title: "Building SQL Builder with Native Java: Simplifying JDBC Code"
weight: 10
authors:
  - sathishk
  - hari-nikesh-r
---

In our previous blog on [API design](/posts/api-design/), we explored the art of creating APIs that are simple, elegant, and optimized. Now, let’s apply those principles to building SQL Builders using plain JDBC in native Java, providing a streamlined approach to working with databases while keeping the code concise and efficient.

**SQL Builders** simplify database interactions by abstracting away raw SQL queries and connection management, allowing developers to focus on business logic. Popular tools like Spring JDBC and QueryDSL help construct SQL queries programmatically, making code cleaner and easier to maintain.

### Motivation
Many developers rely on third-party frameworks like Spring JDBC Template and MyBatis for SQL Builders. Building this functionality natively in Java can offer a lighter, more customizable solution. Let’s design an API for common database operations with plain JDBC.

### Setup

We’ll use an H2 database with the following table:

```sql
CREATE TABLE movie (
    id bigint auto_increment PRIMARY KEY,
    title VARCHAR(80) NOT NULL,
    directed_by VARCHAR(80)
);
```

We configure the `JdbcDataSource` as follows:

```java
JdbcDataSource dataSource = new JdbcDataSource();
dataSource.setURL("jdbc:h2:~/test");
dataSource.setUser("sa");
dataSource.setPassword("sa");
```

We define the `Movie` record:

```java
public record Movie(Long id, String title, String directedBy) {}
```

### Inserting Records

We insert two movie records:

```sql
INSERT INTO movie(title, directed_by) 
      VALUES ('Dunkirk', 'Nolan'),
             ('Inception', 'Nolan');
```

#### JDBC Code for Inserting Records

```java
String sql = "INSERT INTO movie(title, directed_by) VALUES (?, ?), (?, ?)";

try (Connection conn = dataSource.getConnection();
     PreparedStatement ps = conn.prepareStatement(sql)) {
    
    ps.setString(1, "Dunkirk");
    ps.setString(2, "Nolan");
    
    ps.setString(3, "Inception");
    ps.setString(4, "Nolan");
    
    ps.executeUpdate();
}
```

### Querying Records

#### Single Record Query

Query for a single movie by ID:

```sql
SELECT id, title, directed_by FROM movie WHERE id = 1;
```

##### JDBC Code for Single Record Query

```java
String sql = "SELECT id, title, directed_by FROM movie WHERE id = ?";
Movie movie = null;

try (Connection conn = dataSource.getConnection();
     PreparedStatement ps = conn.prepareStatement(sql)) {

    ps.setLong(1, 1);
    try (ResultSet rs = ps.executeQuery()) {
        if (rs.next()) {
            movie = new Movie(rs.getLong("id"), rs.getString("title"), rs.getString("directed_by"));
        }
    }
}
```

#### Multiple Record Query

Query all movies:

```sql
SELECT id, title, directed_by FROM movie;
```

##### JDBC Code for Multiple Record Query

```java
String sql = "SELECT id, title, directed_by FROM movie";
List<Movie> movies = new ArrayList<>();

try (Connection conn = dataSource.getConnection();
     PreparedStatement ps = conn.prepareStatement(sql);
     ResultSet rs = ps.executeQuery()) {

    while (rs.next()) {
        movies.add(new Movie(rs.getLong("id"), rs.getString("title"), rs.getString("directed_by")));
    }
}
```