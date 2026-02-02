# Spring-Boot-REST-API-with-PostgreSQL
---
A professional Spring Boot RESTful API project built using Spring Data JPA, PostgreSQL, and Maven. This project demonstrates complete CRUD operations following the Spring Boot MVC architecture.

## 📌 Features
- RESTful API design
- Spring Boot MVC architecture
- CRUD operations (Create, Read, Update, Delete)
- PostgreSQL database integration
- Spring Data JPA (Hibernate ORM)
- Maven-based project structure
- Tested using Postman

## 🧰 Technology Stack

| Technology        | Description                         |
|-------------------|-------------------------------------|
| Java              | Core programming language            |
| Spring Boot       | Backend framework                   |
| Spring Data JPA   | ORM & database operations            |
| PostgreSQL        | Relational database                 |
| Maven             | Dependency management               |
| Postman           | API testing                         |


## 📂 Project Structure
```
KCAPI
├── src/main/java
│   └── kumlesh
│       ├── KurrecomputersApplication.java
│       ├── Kurre.java
│       ├── Kurrerepo.java
│       └── KurreControler.java
│
├── src/main/resources
│   └── application.properties
└── pom.xml
```

## ⚙️ Project Setup
### 1️⃣ Create Spring Boot Project
- Project Type: Maven
- Group: restapi
- Artifact: KCAPI
- Package: kcrestapi

### 2️⃣ Dependencies Used
- Spring Boot DevTools
- Spring Web
- Spring Data JPA
- PostgreSQL Driver
- Spring Boot Actuator


## 🗄️ Database Configuration
src/main/resources/application.properties
```
spring.application.name=kurrecomputers
spring.datasource.url=jdbc:postgresql://localhost:5432/your_database_name
spring.datasource.username=your_username
spring.datasource.password=YOUR_PASSWORD
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA settings
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

## ▶️ Application Entry Point
```

package kumlesh;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class KurrecomputersApplication {

	public static void main(String[] args) {
		SpringApplication.run(KurrecomputersApplication.class, args);
		System.out.println("Success....!");
	}

}

```
Run the project using: Run As → Spring Boot App

## 🧱 Entity Layer (Model)
@Entity
public class Kurre {
```
	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private int id;
	private String name;
	private String mobile;

	// Getters and Setters
}
```
## 📦 Repository Layer
```
package kumlesh;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import java.util.List;

public interface Kurrerepo extends JpaRepository<Kurre, Integer> {

    @Query(value = "SELECT * FROM employe", nativeQuery = true)
    List<Kurre> getAllEmployees();
}
```
## 🎮 Controller Layer
```
package kumlesh;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController  
// ye ek aisa annotation hai jo REST API ke liye required sabhi methods
// ko handle karta hai. Ye REST API create karne me help karta hai
// jaise: insert, update, delete, select
public class KurreControler {

	@Autowired    
	// @Autowired automatically repository ko inject karta hai,
	// jisse hum database me data get, save, update aur delete
	// jaise operations kar sakte hain
	private Kurrerepo repo;

	 // ---------------------- READ ALL ------------------------
	@GetMapping("/kurre")       //@GetMapping data select karo
    public List<Kurre> findAllBg(){
   	 List<Kurre> list = repo.findAll();
   	 return list;
    }
	// ---------------------- CREATE (INSERT)commen method -----------------
    @PostMapping("/savekurre")
    public Kurre savekurre(@RequestBody Kurre s) {
        return repo.save(s);
    }
    //-------------------response method---------------------------------------
    @PostMapping("/savekurr")
    public Object savekurr(@RequestBody Kurre s) {
        repo.save(s);
        Map<String, Object> response = new HashMap<>();
        response.put("status",  200);
        response.put("Message", "Record Save sucessfully...!!!");
        return response;
    }
    // ---------------------- UPDATE --------------------------
    @PutMapping("/updatekurre")
    public Kurre updateKurre(@RequestBody Kurre p) {
         return repo.save(p);
    }
    //-------------------response method---------------------------------------  
    @PutMapping("/updatekurr")
    public Object updateKurr(@RequestBody Kurre p) {
          repo.save(p);
          Map<String, Object> response = new HashMap<>();
          response.put("status",  200);
          response.put("Message", "Record Update sucessfully...!!!");
          return response;
    }
    // ---------------------- DELETE --------------------------
    @DeleteMapping("/deletekurre/{id}")
    public String deleteKurre(@PathVariable int id) {
        repo.deleteById(id);
        return "Record Deleted Successfully ID = " + id;
    }
    //-------------------response method--------------------------------------- 
    @DeleteMapping("/deletekurr/{id}")
    public Object deleteKurr(@PathVariable int id) {
        repo.deleteById(id);
        Map<String, Object> response = new HashMap<>();
        response.put("status",  200);
        response.put("Message", "Record Delete sucessfully...!!!");
        return response;
    }

}

```
## 🧪 API Endpoints (Postman)
🔹 Get All Records
GET /kurre

🔹 Insert Record
POST /savekurre
```
{
  "name": "test",
  "mobile": "1234567890"
}
```
🔹 Update Record
PUT /updatekurre
```
{
  "id": 2,
  "name": "sahil",
  "mobile": "0987654321"
}
```
🔹 Delete Record
DELETE /deletekurre/{id}

## ✅ Output
- API successfully performs CRUD operations
- Data automatically stored in PostgreSQL
- REST endpoints tested via Postman

## 🎯 Learning Outcome
- Hands-on experience with Spring Boot
- Real-world REST API development
- Database integration using JPA
- Clean MVC architecture understanding

## 👨‍💻 Author

Kumlesh Kurre
Backend Developer | Spring Boot | PostgreSQL
