# Spring Boot in Hindi

## 📚 Chapter 1: Getting Started with Spring Data JPA

### 1.1 Introduction

Backend application banane mein sabse important cheez hoti hai — data ko store, retrieve aur manage karna.

Agar hum traditional JDBC ka use karein, to kaafi manual coding karni padti hai jaise:

| Manual JDBC Tasks          | Spring Data JPA Tasks           |
| -------------------------- | ------------------------------- |
| Database connection banana | Automatic connection management |
| SQL queries likhna         | No SQL needed                   |
| ResultSet handle karna     | Automatic mapping               |

Ye process tedious aur error-prone hota hai.

Spring Data JPA humari life easy bana deta hai. Iske through hum kam code likh ke apne database ke saath kaam kar sakte hain.

### 1.2 Apna Project Kaise Setup Kare?

Spring Data JPA project banana bohot aasaan hai. Do tareeke hain:

| Setup Method       | Steps                                                                                  | Time Required |
| ------------------ | -------------------------------------------------------------------------------------- | ------------- |
| start.spring.io    | 1. Project details bharein<br>2. Dependencies select karein<br>3. Download & import    | 5 minutes     |
| Spring Tools Suite | 1. New → Spring Starter Project<br>2. Details bharein<br>3. Dependencies select karein | 3 minutes     |

✅ 5 minute mein ek ready project mil jata hai.

### 1.3 Example Practice Ke Liye

Agar tumko practice karni hai, to Spring Data ke official examples ka ek repository available hota hai.
Usme kaafi real-world based small projects diye hote hain jaise CRUD operation, custom queries waale.

| Practice Type  | Description      | Best For     |
| -------------- | ---------------- | ------------ |
| CRUD Examples  | Basic operations | Beginners    |
| Custom Queries | Complex queries  | Intermediate |
| Real Projects  | Complete apps    | Advanced     |

✅ Best way seekhne ka hai — khud run kar ke dekhna.

### 1.4 Apna Pehla Spring Data JPA Application (Hello World Example)

Chalo ab ek simple application banate hain — ek entity aur uska repository bana ke.

#### 1.4.1 Entity Class (Person.java)

```java
@Entity
class Person {
  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long id;
  private String name;
  // getters and setters omitted for brevity
}
```

| Annotation      | Purpose                         | Example                          |
| --------------- | ------------------------------- | -------------------------------- |
| @Entity         | Database table se map karta hai | @Entity class Person             |
| @Id             | Primary key banata hai          | @Id private Long id              |
| @GeneratedValue | Auto ID generation              | @GeneratedValue(strategy = AUTO) |

✅ Ab Person class ka har object database mein ek record banega.

#### 1.4.2 Repository Interface (PersonRepository.java)

```java
interface PersonRepository extends Repository<Person, Long> {
  Person save(Person person);
  Optional<Person> findById(long id);
}
```

| Method     | Purpose            | Return Type      |
| ---------- | ------------------ | ---------------- |
| save()     | Save/update person | Person           |
| findById() | Find by ID         | Optional<Person> |

✅ Tum easily apne data ko store aur fetch kar sakte ho without SQL.

#### 1.4.3 Main Application Class (DemoApplication.java)

```java
@SpringBootApplication
public class DemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(DemoApplication.class, args);
  }

  @Bean
  CommandLineRunner runner(PersonRepository repository) {
    return args -> {
      Person person = new Person();
      person.setName("John");
      repository.save(person);
      Person saved = repository.findById(person.getId())
                    .orElseThrow(NoSuchElementException::new);
    };
  }
}
```

| Annotation             | Purpose                            | Example                                      |
| ---------------------- | ---------------------------------- | -------------------------------------------- |
| @SpringBootApplication | Spring Boot app identify karta hai | @SpringBootApplication class DemoApplication |
| @Bean                  | Spring bean define karta hai       | @Bean CommandLineRunner                      |
| CommandLineRunner      | Application start pe run hota hai  | CommandLineRunner runner()                   |

✅ Pura ek chhota sa CRUD operation ka flow ready hai.

### 1.5 Important Points

| Point               | Description                                     | Example                                |
| ------------------- | ----------------------------------------------- | -------------------------------------- |
| Auto Implementation | Repository ka implementation automatic hota hai | No need to write implementation class  |
| Auto Wiring         | @Autowired/@Bean ke through injection           | @Autowired PersonRepository repository |
| CommandLineRunner   | Startup time pe kaam karne ke liye              | @Bean CommandLineRunner                |
| Optional Handling   | Record fetch karte waqt important               | Optional<Person> findById()            |

### 1.6 Extra Knowledge

Spring Data JPA mein different type ke repository interfaces available hain:

| Interface Name     | Features                    | Best For    |
| ------------------ | --------------------------- | ----------- |
| Repository         | Basic operations            | Simple apps |
| CrudRepository     | CRUD operations             | Small apps  |
| ListCrudRepository | CRUD + List operations      | Medium apps |
| JpaRepository      | CRUD + Pagination + Sorting | Large apps  |

✅ Small project ke liye Repository aur CrudRepository kaafi hote hain.
✅ Big projects mein mostly JpaRepository ka use hota hai.

## 📖 Chapter 1 Summary

| Topic            | Summary                                                        |
| ---------------- | -------------------------------------------------------------- |
| Project Setup    | start.spring.io ya STS se project create karna                 |
| Entity Class     | Database table ka Java class representation                    |
| Repository       | Database operations ko manage karta hai                        |
| Main Class       | Application ko run karne ka flow set karta hai                 |
| Important Points | Auto-wiring, Auto-implementation aur Optional handling ka role |

## 📝 Chapter 1: 20 Questions (Practice / Assignment)

### Basic Questions

1. Spring Data JPA kya hai aur iska main use kya hai?

2. Apna Spring Boot project kaise create kar sakte hain?

3. Project setup ke liye kaun kaun se dependencies jaruri hoti hain?

4. `@Entity` annotation ka kya role hai?

5. `@Id` aur `@GeneratedValue` annotations kis liye use hote hain?

6. Repository interface banana kyun zaruri hai?

7. PersonRepository mein `save()` aur `findById()` methods kya karte hain?

8. Spring Data JPA mein repository ka implementation kaun karta hai?

9. CommandLineRunner ka kya use hota hai application mein?

10. Optional class ka kya role hai `findById()` method ke sath?

### Thoda Advance Thinking

11. `@SpringBootApplication` annotation ke andar kya kya hota hai?

12. start.spring.io aur STS dono mein kya difference hai project banate waqt?

13. Spring automatically repository instances ko kaise inject karta hai?

14. Agar `findById()` se record nahi mile to kya hota hai?

15. Hum manually implementation class kyun nahi banate Spring Data JPA mein?

16. H2 Database aur MySQL database mein kya major difference hai development ke time pe?

17. Agar kisi Entity mein `@Entity` annotation nahi lagaye to kya error aayega?

18. Spring Data JPA mein Repository, CrudRepository, aur JpaRepository mein kya differences hain?

19. ListCrudRepository ka kab use karte hain?

20. Hello World example mein agar database connection galat ho jaye to application kaise behave karegi?

## 📚 Core Concepts of Spring Data JPA — Ekdum Seedha aur Clear Hindi mein

### 1. Repository Interface kya hai?

Repository ek main interface hai.

Ye batata hai kaunsi Entity class (jaise User, Student) aur kaunsa ID type (Long, Integer) manage karna hai.

Repository bas types ko capture karta hai aur aage ka kaam Spring Data karta hai.

### 2. Entity ya Domain Type kya hai?

Entity ka matlab hai — koi object jo database mein ek record banega.

Entity ka apna ek ID (Primary Key) hota hai.

Domain Object ya Aggregate bhi same hi hote hain (Entity jaise hi).

### 3. Domain Driven Design (DDD) ka matlab

Har Entity ka ek ID hota hai.

Hum jab database se Entity nikalte hain ya save karte hain to ID ka use karte hain.

Spring DDD ka concept follow karta hai.

### 4. CrudRepository Interface kya hai?

CrudRepository ek interface hai jo basic CRUD operations deta hai:

```java
public interface CrudRepository<T, ID> extends Repository<T, ID> {
  <S extends T> S save(S entity);
  Optional<T> findById(ID primaryKey);
  Iterable<T> findAll();
  long count();
  void delete(T entity);
  boolean existsById(ID primaryKey);
}
```

Iske method ka simple meaning:

- `save(entity)` ➔ Entity ko save/update karta hai.
- `findById(id)` ➔ ID ke base pe ek Entity fetch karta hai.
- `findAll()` ➔ Saari Entities laata hai.
- `count()` ➔ Total kitni Entities hai, batata hai.
- `delete(entity)` ➔ Entity ko delete karta hai.
- `existsById(id)` ➔ Check karta hai ki ID exist karti hai ya nahi.

### 5. ListCrudRepository kya hai?

ListCrudRepository bhi wahi CRUD methods deta hai.

Farak sirf itna hai: ye List return karta hai, Iterable nahi.

### 6. Reserved Methods ka kya matlab hai?

Kuch methods jaise `findById(ID)` predefined hote hain.

Tumhe khud query nahi likhni padti.

Spring khud samajh leta hai ki kis ID pe kaam karna hai.

### 7. @Query Annotation kab use karte hain?

Jab tumhara Entity ka ID ka naam kuch alag hai (jaise userCode) aur confusion ho raha ho, tab tum @Query likh sakte ho.

Lekin recommend kiya jata hai ki normal id naming follow karo, warna error aasakta hai.

### 8. JpaRepository aur MongoRepository kya hote hain?

- JpaRepository ➔ SQL databases ke liye (jaise MySQL, Postgres).
- MongoRepository ➔ MongoDB ke liye (NoSQL database).

Dono CrudRepository ko extend karte hain aur extra features dete hain.

### 9. PagingAndSortingRepository kya karta hai?

Agar tumko data ko page-by-page ya sorted format mein chahiye, to ye interface use karte hain.

Methods:

- `findAll(Sort sort)` ➔ Sorting ke saath data laata hai.
- `findAll(Pageable pageable)` ➔ Pagination ke saath data laata hai.

Example:
Page 2, 20 records per page:

```java
Page<User> users = repository.findAll(PageRequest.of(1, 20));
```

### 10. ListPagingAndSortingRepository kya karta hai?

Same jaise PagingAndSortingRepository.

Farak sirf itna hai: Ye List return karta hai, Iterable nahi.

### 11. Derived Count Query kya hoti hai?

Agar tum count karna chahte ho based on kisi property:

```java
interface UserRepository extends CrudRepository<User, Long> {
  long countByLastname(String lastname);
}
```

✅ Matlab: Lastname ke base pe kitne users hain, count karo.

### 12. Derived Delete Query kya hoti hai?

Agar tum delete karna chahte ho based on property:

```java
interface UserRepository extends CrudRepository<User, Long> {
  long deleteByLastname(String lastname);
  List<User> removeByLastname(String lastname);
}
```

✅ Matlab: Lastname ke base pe users delete kar do.

## 🔥 Real-World Usage of Methods with Examples

### 1. save(entity)

**Kaam:**

- Naya record create karna
- Ya existing record ko update karna

**Example:**

```java
Student student = new Student();
student.setName("Ravi");
student.setClassName("10th");

studentRepository.save(student);
```

**Yaha:**

- Agar student ka ID null hai → to naya student insert hoga
- Agar student ka ID already database me hai → to record update hoga

### 2. findById(id)

**Kaam:**

- Kisi particular ID ka student record laana

**Example:**

```java
Optional<Student> studentOpt = studentRepository.findById(1L);

if (studentOpt.isPresent()) {
    Student student = studentOpt.get();
    System.out.println(student.getName());
}
```

**Yaha:**

- ID 1 ke student ka naam print hoga agar student database me hoga

### 3. findAll()

**Kaam:**

- Sabhi students ka list laana

**Example:**

```java
List<Student> students = (List<Student>) studentRepository.findAll();
for (Student st : students) {
    System.out.println(st.getName());
}
```

**Yaha:**

- Database ke saare students ke naam print honge

### 4. deleteById(id)

**Kaam:**

- Kisi specific ID ka record delete karna

**Example:**

```java
studentRepository.deleteById(5L);
```

**Yaha:**

- ID = 5 waale student ka record database se delete ho jaayega

### 5. delete(entity)

**Kaam:**

- Direct ek entity ko delete karna

**Example:**

```java
Student student = studentRepository.findById(2L).get();
studentRepository.delete(student);
```

**Yaha:**

- Pehle ID 2 waala student laaya, fir usko delete kiya

### 6. count()

**Kaam:**

- Database me total kitne students hain, uska count batana

**Example:**

```java
long totalStudents = studentRepository.count();
System.out.println("Total Students: " + totalStudents);
```

### 7. existsById(id)

**Kaam:**

- Check karna ki koi ID database me hai ya nahi

**Example:**

```java
boolean exists = studentRepository.existsById(3L);
if (exists) {
    System.out.println("Student exists");
} else {
    System.out.println("Student does not exist");
}
```

## ✅ Method Summary Table

| Method Name    | Kaam (Kya karta hai)                       | Kab Use Karte hain                                  |
| -------------- | ------------------------------------------ | --------------------------------------------------- |
| save(entity)   | Entity ko save/update karta hai            | Naya record create ya existing update karne ke liye |
| findById(id)   | ID se ek record dhoondta hai               | Specific record fetch karne ke liye                 |
| findAll()      | Sabhi records ko laata hai                 | Saare records ko list me lene ke liye               |
| deleteById(id) | ID se record ko delete karta hai           | Specific record delete karne ke liye                |
| delete(entity) | Entity object delete karta hai             | Object ko directly delete karne ke liye             |
| count()        | Total records ka count deta hai            | Total records ka number nikalne ke liye             |
| existsById(id) | Check karta hai ID exist karti hai ya nahi | Record existence check karne ke liye                |

## 🔥 Repository Interface Types

### 1. Basic Repository

```java
interface UserRepository extends Repository<User, Long> {}
```

### 2. CRUD Repository

```java
interface StudentRepository extends CrudRepository<Student, Long> {}
```

### 3. List CRUD Repository

```java
interface StudentRepository extends ListCrudRepository<Student, Long> {}
```

### 4. Reactive Repository

```java
interface ReactiveStudentRepository extends ReactiveCrudRepository<Student, Long> {}
```

### 5. Paging and Sorting Repository

```java
interface StudentRepository extends PagingAndSortingRepository<Student, Long> {}
```

### 6. Custom Base Repository

```java
@NoRepositoryBean
interface MyBaseRepository<T, ID> extends Repository<T, ID> {
    Optional<T> findById(ID id);
    <S extends T> S save(S entity);
}
```

## 🔥 Multiple Database Handling

### 1. JPA Repository

```java
interface MyRepository extends JpaRepository<User, Long> {}
```

### 2. MongoDB Repository

```java
interface UserRepository extends MongoRepository<User, Long> {}
```

### 3. Configuration for Multiple Databases

```java
@EnableJpaRepositories(basePackages = "com.acme.repositories.jpa")
@EnableMongoRepositories(basePackages = "com.acme.repositories.mongo")
class Configuration {}
```

## 📝 Key Points to Remember

1. Repository interface define karte waqt Entity type aur ID type specify karna important hai
2. CrudRepository extend karne se basic CRUD operations mil jaate hain
3. ListCrudRepository Iterable ki jagah List return karta hai
4. Multiple databases use karne ke liye proper configuration zaruri hai
5. @NoRepositoryBean ka use base interfaces ke liye hota hai
6. Reactive applications ke liye ReactiveCrudRepository use karna chahiye
7. Pagination aur sorting ke liye PagingAndSortingRepository use karna chahiye

## 📖 Full Summary (One-Table mein)

| Concept                    | Simple Meaning                          |
| -------------------------- | --------------------------------------- |
| Repository                 | Entity + ID manage karta hai            |
| Entity                     | Database ka ek record                   |
| CrudRepository             | Basic save, find, delete, count methods |
| ListCrudRepository         | CRUD + List return karta hai            |
| JpaRepository              | JPA (SQL) ke liye extra features        |
| PagingAndSortingRepository | Pagination aur sorting ke liye          |
| @Query                     | Jab custom query likhni ho              |
| countBy.., deleteBy..      | Automatic query banane ke liye          |

## 📝 Practice Questions

### Core Concepts Questions

1. Repository interface ka main kaam kya hai?
2. Repository mein hum kaunse do types define karte hain?
3. Entity kya hoti hai?
4. Domain Object aur Entity mein kya relation hai?
5. Value Object kya hota hai? Entity se kaise alag hai?
6. CrudRepository interface kya karta hai?
7. save() method ka kya kaam hai CrudRepository mein?
8. findById() method ka use kya hai?
9. findAll() method kya return karta hai?
10. count() method ka kya kaam hai?
11. ListCrudRepository aur CrudRepository mein kya fark hai?
12. @Query annotation kab use karte hain?
13. Agar Entity ka ID field ka naam id nahi hai, to kya dikkat ho sakti hai?
14. JpaRepository kis ke liye use hota hai?
15. MongoRepository kis ke liye use hota hai?
16. PagingAndSortingRepository ka kya kaam hai?
17. findAll(Pageable pageable) kya karta hai?
18. Derived Query ka matlab kya hota hai?
19. countByLastname() method kis kaam me aata hai?
20. deleteByLastname() aur removeByLastname() mein kya fark hai?

### 📖 Bonus Short Questions (1 line wale)

1. Repository kis package mein hoti hai Spring Data mein?
2. Kaunsa method database se ek record delete karta hai CrudRepository mein?
3. Entity ko identify karne ke liye kis annotation ka use hota hai?
4. Paging aur Sorting karne ke liye kaunsa repository use hoti hai?

## 📝 20–30 Important Questions on Spring Data JPA Repository

### Concept Understanding Questions (Theory)

1. Repository interface kya hoti hai Spring Data JPA me?

2. Repository banate waqt kaunsi 2 cheezein specify karni padti hai?

3. Agar tumhe CRUD operations chahiye to kaunsa interface extend karoge?

4. ListCrudRepository aur CrudRepository me kya difference hai?

5. Reactive programming ke liye kaunsa repository interface use hota hai?

6. Kotlin projects ke liye kaunsa repository interface use kiya jata hai?

7. PagingAndSortingRepository kis kaam me aata hai?

8. @RepositoryDefinition ka kya use hai?

9. Agar sirf kuch selected methods expose karne ho to kya karna padega?

10. @NoRepositoryBean annotation ka kya role hai?

### Code-Based Practical Questions

1. Student entity ke liye ek simple CRUD Repository interface ka code likho.

2. Kisi student ko database me save karne ka code likho using repository.

3. Student ko ID ke basis par database se kaise fetch karoge? Code likho.

4. Kaise check karoge ki koi student ID exist karta hai ya nahi?

5. Student ka record database se delete karne ka code likho (ID ke basis pe).

6. Sabhi students ko database se fetch karne ka code likho.

### Deep Concept Check

1. save() method new entity aur existing entity me kaise behave karta hai?

2. Agar kisi entity ka ID null hai to save() method kya karega?

3. Agar kisi entity ka ID existing hai to save() method kya karega?

4. findById() method ka return type kya hota hai? Kyu?

5. Agar findById() se koi record nahi milta to kya hota hai?

### Real-World Usecase-Based Questions

1. Agar ek project me JPA aur MongoDB dono use ho rahe ho, to repository kaise distinguish karoge?

2. Entity ke upar @Entity aur @Document dono lagane se kya dikkat hoti hai?

3. Kaise multiple repositories ke base packages define karte hain?

4. Spring Data me custom queries likhne ke liye kya kar sakte ho?

### MCQ (Multiple Choice Questions)

1. CrudRepository kis package me hota hai?

   - (a) org.springframework.data.repository
   - (b) org.springframework.data.jpa.repository
   - (c) org.hibernate.repository
   - (d) org.springframework.boot.repository
     ✅ Answer: (a)

2. findById() ka return type kya hota hai?

   - (a) Entity
   - (b) Optional<Entity>
   - (c) List<Entity>
   - (d) Boolean
     ✅ Answer: (b)

3. deleteById() method kya return karta hai?

   - (a) boolean
   - (b) void
   - (c) int
   - (d) String
     ✅ Answer: (b)

4. Agar tum List return karna chahte ho to kaunsa repository extend karoge?

   - (a) CrudRepository
   - (b) ListCrudRepository
   - (c) JpaRepository
   - (d) MongoRepository
     ✅ Answer: (b)

5. PagingAndSortingRepository kis liye use hota hai?
   - (a) CRUD
   - (b) Sort aur Pagination
   - (c) Validation
   - (d) Security
     ✅ Answer: (b)

### ✅ Bonus: 5 Extra Practice Questions (Advanced Thinking)

1. Tum apne khud ke custom base repository ko kaise design karoge?

2. Agar kisi repository me findAll() override karna ho to kaise karoge?

3. ReactiveCrudRepository me save() method ka return type kya hota hai?

4. CRUD methods ko selective expose karne ka practical advantage kya hai?

5. CrudRepository aur JpaRepository me kya difference hai?

## 📚 Final Summary

| Type              | Questions |
| ----------------- | --------- |
| Concept Theory    | 10        |
| Code Practical    | 6         |
| Deep Thinking     | 5         |
| Real-World Design | 4         |
| MCQ               | 5         |
| Bonus Practice    | 5         |

## ✨ Spring Data JPA Configuration - Full Easy Explanation

### 🔵 Configuration Introduction

Spring Data JPA ko configure karne ke 2 tareeke hain:

- Java annotations (@EnableJpaRepositories waale)
- XML file likh ke (`<jpa:repositories>`) ke through.

### 🔵 Annotation-based Configuration

Tum Java ke annotations ya XML dono se apne JPA repositories activate kar sakte ho.

#### 🛠 Example 1: JavaConfig

```java
@Configuration
@EnableJpaRepositories
@EnableTransactionManagement
class ApplicationConfig {
```

- `@Configuration` ➔ Batata hai ki ye ek Spring Configuration class hai
- `@EnableJpaRepositories` ➔ Batata hai ki yaha JPA repositories ka auto-scanning start karo
- `@EnableTransactionManagement` ➔ Transaction management enable karta hai (begin, commit, rollback)

```java
@Bean
public DataSource dataSource() {
    EmbeddedDatabaseBuilder builder = new EmbeddedDatabaseBuilder();
    return builder.setType(EmbeddedDatabaseType.HSQL).build();
}
```

- **DataSource** ➔ Ye batata hai ki kaunsa database hum use karenge (HSQLDB yaha example me ek in-memory DB hai)

```java
@Bean
public LocalContainerEntityManagerFactoryBean entityManagerFactory() {
    HibernateJpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
    vendorAdapter.setGenerateDdl(true);

    LocalContainerEntityManagerFactoryBean factory = new LocalContainerEntityManagerFactoryBean();
    factory.setJpaVendorAdapter(vendorAdapter);
    factory.setPackagesToScan("com.acme.domain");
    factory.setDataSource(dataSource());
    return factory;
}
```

- **EntityManagerFactory** ➔ Ye entity classes ko database me map karta hai
- Hibernate ko bataya jaa raha hai ki DDL (Create Table, Alter Table) generate karna hai
- EntityManagerFactory ko configure kiya gaya hai:
  - Hibernate adapter set kiya
  - Entity classes ke package bataye
  - Database connection diya

```java
@Bean
public PlatformTransactionManager transactionManager(EntityManagerFactory entityManagerFactory) {
    JpaTransactionManager txManager = new JpaTransactionManager();
    txManager.setEntityManagerFactory(entityManagerFactory);
    return txManager;
}
```

- **TransactionManager** ➔ Database transactions manage karega
- JPA ke saath `JpaTransactionManager` use hota hai

### 🔵 Important Point:

Direct `EntityManagerFactory` mat banao, kyunki `LocalContainerEntityManagerFactoryBean` hi Exception translation support karta hai, jo Spring ke liye important hai.

### 🔵 Spring Namespace (XML configuration)

Spring Data JPA ek alag XML namespace deta hai jisse tum repositories declare kar sakte ho.

#### 🛠 Example 2: XML Configuration

```xml
<jpa:repositories base-package="com.acme.repositories" />
```

- `base-package` ➔ Wo package jisme tumhari repository interfaces rakhe gaye hain

### 🔵 JavaConfig vs XML Config — Which is Better?

- Pehle ke zamane me XML use hota tha (Spring 2.x)
- Aaj ke time me JavaConfig zyada popular hai (`@Configuration`, `@EnableJpaRepositories`)
- Future me naye features sirf JavaConfig me mil sakte hain, XML me nahi

### 🔵 Exception Translation

Jab tum `<jpa:repositories>` ya `@EnableJpaRepositories` use karte ho, Spring automatic database errors ko apne standard errors me convert karta hai jaise `DataAccessException`.

### 🔵 Custom Namespace Attributes

Agar tumhare project me multiple `EntityManagerFactory` ya multiple `TransactionManager` hain to tum manually specify kar sakte ho.

| Attribute                    | Kya Karta Hai                                              | Kab Zarurat Padegi          |
| :--------------------------- | :--------------------------------------------------------- | :-------------------------- |
| `entity-manager-factory-ref` | Konsa EntityManagerFactory use karna hai specify karta hai | Jab multiple factories hain |
| `transaction-manager-ref`    | Konsa transaction manager use karna hai specify karta hai  | Jab multiple managers hain  |

### 🔵 Bootstrap Mode (Spring Data JPA 2.1+)

- Normal default me repositories start hote hi ban jaate hain (early initialization)
- **Background thread** se EntityManagerFactory initialize karne ke liye kuch naya mode diya gaya hai:

| Mode       | Matlab                                                                                        |
| :--------- | :-------------------------------------------------------------------------------------------- |
| `DEFAULT`  | Repositories turant ban jaate hain jab jarurat ho                                             |
| `LAZY`     | Repositories tabhi banenge jab actual use karoge                                              |
| `DEFERRED` | Repositories tab banenge jab application poora load ho jaye (`ContextRefreshedEvent` ke baad) |

### 🔵 Recommendations

- Agar tum normal synchronous initialization kar rahe ho ➔ DEFAULT best hai
- Agar JPA ko asynchronously load kar rahe ho ➔ DEFERRED use karo
- Testing me ya development time me ➔ LAZY mode achha hai (fast startup ke liye)

## 🎯 Practice Questions

### 📘 Concept Questions

1. Spring Data JPA ko configure karne ke kitne tareeke hain?
2. @EnableJpaRepositories annotation ka kya kaam hai?
3. LocalContainerEntityManagerFactoryBean kyun banana padta hai?
4. DataSource bean kis cheez ke liye banate hain?
5. HibernateJpaVendorAdapter kya karta hai?
6. EntityManagerFactory kya kaam karta hai Spring me?
7. @EnableTransactionManagement kyun lagate hain?
8. PlatformTransactionManager ka kya role hai?

### 📘 Code Based Practical

9. JavaConfig ka example likho jisme H2 database use ho
10. XML me JPA repositories ka declaration kaise karoge?
11. Spring XML me base-package kya kaam karta hai?
12. Spring XML me EntityManagerFactory specify karne ka tarika kya hai?

### 📘 Concept Deep Dive

13. JavaConfig aur XML config me kya difference hai?
14. JavaConfig kyu zyada preferred hai aaj ke time me?
15. Spring Data JPA me Exception Translation ka kya benefit hai?
16. Agar multiple EntityManagerFactory hai to kya karoge?
17. Agar multiple transaction managers hain to kya karoge?

### 📘 Bootstrap Mode Pe Questions

18. BootstrapMode DEFAULT kya karta hai?
19. BootstrapMode LAZY kaise kaam karta hai?
20. BootstrapMode DEFERRED ka kya benefit hai?
21. Agar tum asynchronous JPA bootstrap kar rahe ho to kaunsa bootstrap mode sahi hai?
22. Testing ya local development ke liye kaunsa bootstrap mode use karoge?

### 📘 MCQ Type Short Questions

23. LocalContainerEntityManagerFactoryBean ka alternative kya hota hai?
24. Kaunsa annotation repositories ko scan karne lagata hai?
25. Kaunsa exception class JPA errors ko wrap karti hai Spring me?
26. BootstrapMode me DEFERRED kaam kaise karta hai internally?
27. Spring Data JPA me PlatformTransactionManager ka default naam kya hai?

### 📘 Real World Scenarios

28. Agar application me ek MongoDB aur ek JPA database dono hain to kya dikkat aa sakti hai?
29. EntityManagerFactory late initialize karne ka kya fayda hai?
30. JavaConfig me agar base package nahi diya to kaunsa package scan hota hai?

## 📚 Final Summary

| Type                     | Questions |
| ------------------------ | --------- |
| Concept Questions        | 8         |
| Code Based Practical     | 4         |
| Concept Deep Dive        | 5         |
| Bootstrap Mode Questions | 5         |
| MCQ Type Questions       | 5         |
| Real World Scenarios     | 3         |

## ✨ Persisting Entities - Full Easy Explanation

### 🔵 Introduction

Yeh section batata hai ki **Spring Data JPA** me entity (jaise `Student`, `Order`) ko **database me kaise save karte hain**.

### 🔵 Saving Entities

Entity ko database me save karne ke liye hum **`CrudRepository.save()`** method ka use karte hain.

Backend me `save()` method **EntityManager** ka use karta hai:

- Agar nayi entity hai ➔ `entityManager.persist()`
- Agar existing entity hai ➔ `entityManager.merge()`

### 🔵 Entity State-detection Strategies

Spring Data ko yeh samajhna padta hai ki **entity nayi hai ya purani**.  
Iske liye kuch strategies hoti hain.

#### Strategy 1: Version-Property and ID Inspection (Default)

- Pehle yeh check karta hai ki kya entity me koi `@Version` field hai (non-primitive jaise `Long`, `Integer`, etc)
- Agar version field null hai ➔ entity nayi hai
- Agar Version property nahi hai, to phir ID check karta hai:
  - Agar ID null hai ➔ nayi entity
  - Agar ID non-null hai ➔ purani entity

**Note:** JPA ke according, 0 bhi valid version hota hai. Isliye agar Version field primitive type (`int`, `long`) ka hai, to woh detect karna mushkil hota hai ki naya hai ya nahi.

#### Strategy 2: Implementing Persistable Interface

Agar entity class me tum `Persistable` interface implement karte ho, to Spring tumhari `isNew()` method se samjhega ki entity nayi hai ya purani.

#### Strategy 3: Customizing EntityInformation

Agar tum chaaho, to apna custom EntityInformation bana sakte ho (advance level customization).  
Usually jarurat nahi padti.

### 🔵 Special Case: Manually Assigned Identifiers

Agar tum entity ka ID khud assign karte ho (auto-generate nahi karte), aur Version property nahi hai, tab normal ID check wali strategy kaam nahi karegi.

Is situation me, ek **`isNew` flag** maintain karte hain jo batata hai ki entity nayi hai ya nahi.

#### 🛠 Example: Base Class with isNew Flag

```java
@MappedSuperclass
public abstract class AbstractEntity<ID> implements Persistable<ID> {

  @Transient
  private boolean isNew = true;

  @Override
  public boolean isNew() {
    return isNew;
  }

  @PrePersist
  @PostLoad
  void markNotNew() {
    this.isNew = false;
  }
}
```

**Simple Explanation:**

- `@Transient` ➔ `isNew` field ko database me save nahi karna
- `isNew()` method ➔ batata hai ki entity nayi hai ya purani
- `@PrePersist` aur `@PostLoad` ➔ Jab entity database me save ya load hoti hai, tab `isNew = false` karte hain

### 🔥 Short Full Flow of Persisting Entities:

```plaintext
save(entity)
    |
Check if new:
    - Version field check
    - ID check
    - Persistable.isNew() check
    |
If new ➔ entityManager.persist(entity)
If old ➔ entityManager.merge(entity)
```

## 🎯 Practice Questions

### 📘 Concept Understanding

1. Entity ko Spring Data JPA me kaise save karte hain?
2. CrudRepository.save() method backend me kis JPA method ka use karta hai?
3. persist() aur merge() me kya difference hai?
4. Kaise decide hota hai ki entity nayi hai ya purani?
5. Version-property kya hoti hai aur kaise kaam karti hai?
6. ID field ke basis pe kaise pata lagate hain ki entity nayi hai?
7. Primitive Version fields (int, long) me kya dikkat hoti hai?
8. Persistable interface ka kya role hai?
9. isNew() method kis case me override karte hain?
10. EntityInformation kya customize kar sakte hain?

### 📘 Code-Based Practical

11. Ek entity class likho jisme Persistable implement kiya gaya ho
12. PrePersist aur PostLoad annotations ka kya use hai? Code example do
13. AbstractEntity base class ka example likho jisme isNew flag ho
14. Agar manually assigned ID hai to entity ka new detection kaise karoge?

### 📘 Deep Thinking Questions

15. Jab entity me Version aur ID dono nahi hain, to kya hoga?
16. Spring Data JPA kis situation me entityManager.merge() call karta hai?
17. Agar kisi entity me Version field 0 set hai to kya ye new entity hogi?
18. Custom EntityInformation kyun aur kaise banate hain?

### 📘 Real World Use-Case

19. Agar application me sabhi entities me manually assigned IDs hain to kaunsa pattern follow karoge?
20. Persistable implement karne ke kya advantages aur disadvantages hain?
21. EntityManager.persist() kab automatic call hota hai?

### 📘 MCQ Style Questions

22. Spring Data JPA me save() ke andar new entity ke liye kya method call hota hai?

- (a) persist()
- (b) merge()
- (c) saveOrUpdate()
- (d) refresh()
  ✅ Answer: (a)

23. EntityInformation customize karne ke liye kis class ko extend karna padta hai?

- (a) JpaRepository
- (b) JpaRepositoryFactory
- (c) EntityManagerFactory
- (d) CrudRepository
  ✅ Answer: (b)

24. @PrePersist kab call hota hai?

- (a) Entity save hone ke baad
- (b) Entity save hone se pehle
- (c) Entity load hone ke baad
- (d) Delete hone ke pehle
  ✅ Answer: (b)

25. isNew() method kis interface me defined hai?

- (a) Persistable
- (b) Serializable
- (c) EntityListener
- (d) JpaRepository
  ✅ Answer: (a)

26. Agar ek entity ka ID null nahi hai aur Version field nahi hai, to entity ko kaise treat kiya jaayega?

- (a) New
- (b) Existing
  ✅ Answer: (b)

### 📘 Bonus Tough Questions

27. Manually assigned ID ke case me transient isNew flag kyun zaruri hai?
28. PostLoad annotation ka kya role hai entity life cycle me?
29. Persistable implement karne par entity ka lifecycle kaise control kar sakte ho?
30. EntityManagerFactory ka persist vs merge decision internally kaise hota hai?

## 📚 Final Summary

| Topic                                      | Cover hua? |
| :----------------------------------------- | :--------- |
| Saving entity via save() method            | ✅         |
| persist() vs merge()                       | ✅         |
| How Spring JPA checks entity is new or not | ✅         |
| Version property and ID inspection         | ✅         |
| Persistable interface use                  | ✅         |
| Base entity class with isNew flag          | ✅         |
| 30+ Questions for complete practice        | ✅         |

## ✨ Query Methods ke Return Types

### 🔵 Normal Return Types - List, Iterable, Set

Agar tumhara query multiple records laata hai, tum normally `List`, `Iterable`, ya `Set` return kar sakte ho.

Example:

```java
List<User> findByLastname(String lastname);
Iterable<User> findByCity(String city);
Set<User> findByRole(String role);
```

✅ Ye simple hai, sabhi records ek baar me load ho jaate hain.

### 🔵 Streamable Return Type

- `Streamable` ek special type hai jo **Iterable** ki tarah behave karta hai + extra features deta hai.
- Tum `filter()`, `map()`, jaise operations directly kar sakte ho.

Example:

```java
Streamable<User> findByFirstnameContaining(String firstname);
Streamable<User> findByLastnameContaining(String lastname);
```

Aur fir combine kar sakte ho:

```java
Streamable<User> result =
    repository.findByFirstnameContaining("av")
              .and(repository.findByLastnameContaining("ea"));
```

### 🔵 Custom Streamable Wrapper Types

Tum apna custom return type bhi bana sakte ho, jo `Streamable` ko wrap kare.

Example:

```java
@RequiredArgsConstructor(staticName = "of")
class Products implements Streamable<Product> {

  private final Streamable<Product> streamable;

  public MonetaryAmount getTotal() {
    return streamable.stream()
      .map(Product::getPrice)
      .reduce(Money.of(0), MonetaryAmount::add);
  }

  @Override
  public Iterator<Product> iterator() {
    return streamable.iterator();
  }
}
```

Repository:

```java
interface ProductRepository extends Repository<Product, Long> {
  Products findAllByDescriptionContaining(String text);
}
```

✅ Tum Products object ko direct query se laa sakte ho bina manual wrapping ke.

### 🔵 Stream Return Type (Java 8+)

Agar tumhara data bahut bada hai aur tum ek-ek record process karna chahte ho (batch processing type), to `Stream<T>` use kar sakte ho.

Example:

```java
@Query("select u from User u")
Stream<User> findAllByCustomQueryAndStream();
```

Stream use karte waqt:

```java
try (Stream<User> stream = repository.findAllByCustomQueryAndStream()) {
    stream.forEach(user -> System.out.println(user.getName()));
}
```

✅ **Important:** Stream close karna zaruri hai (try-with-resources).

### 🔵 Asynchronous Query Results

Tum apne query ko async bhi bana sakte ho, jaise:

```java
@Async
Future<User> findByFirstname(String firstname);

@Async
CompletableFuture<User> findOneByFirstname(String firstname);
```

✅ Query background thread me chalegi, aur result Future/CompletableFuture me milega.

### 🔵 Paging aur Slicing (Page, Slice)

Agar result **bohot bada** ho, to paging/slicing ka use karte hain:

#### Page:

```java
Page<User> findByLastname(String lastname, Pageable pageable);
```

- Full page result deta hai
- Page number, size aur total pages ka info deta hai

#### Slice:

```java
Slice<User> findByLastname(String lastname, Pageable pageable);
```

- Sirf current slice deta hai (itna batata hai ki aage aur data hai ya nahi)
- Count query nahi chalti (faster)

### 🔵 Sort aur Limit Special Handling

- Sort:

```java
List<User> findByLastname(String lastname, Sort sort);
```

- Limit:

```java
List<User> findFirst10ByLastname(String lastname);
List<User> findTop5ByAgeGreaterThan(int age);
```

✅ Limit aur Top ka use kar ke **fixed number of results** fetch kar sakte ho.

### 🔵 Big Table for Summary:

| Return Type        | Kaam                           | Special Note                         |
| :----------------- | :----------------------------- | :----------------------------------- |
| List<T>            | Sare results load karta hai    | Memory heavy                         |
| Streamable<T>      | Iterable + stream operations   | Convenient but still all memory      |
| Stream<T>          | Data ek ek karke load hota hai | Stream close karna padta hai         |
| Page<T>            | Full page + total elements     | Costly count query                   |
| Slice<T>           | Only current slice             | Fast, no count query                 |
| Flux<T> (Reactive) | Streaming reactive data        | MongoDB, R2DBC jaise modules ke liye |

## 🎯 Practice Questions

### 📘 Concept Understanding

1. Query method ka return type List kyun use karte hain?
2. Streamable me kya advantage milta hai Iterable ke comparison me?
3. Stream<T> kaise kaam karta hai?
4. Stream close karna kyun zaruri hai?
5. Page aur Slice me kya farak hai?

### 📘 Code Based Practical

6. UserRepository me method likho jo Page<User> return kare.
7. UserRepository me method likho jo Streamable<User> return kare.
8. ProductRepository me method likho jo custom Products type return kare.
9. EmployeeRepository me method likho jo Stream<Employee> return kare.
10. OrderRepository me method likho jo Top 5 Orders fetch kare.

### 📘 Deep Thinking

11. Streamable aur Stream me kya difference hai?
12. Slice kab prefer karoge instead of Page?
13. List return karte waqt kya dikkat aa sakti hai?
14. Future aur CompletableFuture ka kya difference hai asynchronous query me?
15. Pageable aur Sort parameters method me kaise pass karte hain?

### 📘 MCQ Type

16. Streamable kis feature ko support karta hai?

    - (a) Stream operations
    - (b) Async operations
      ✅ Answer: (a)

17. Pageable kis return type ke saath use hota hai?

    - (a) Page
    - (b) List
      ✅ Answer: (a)

18. Slice me kya missing hota hai jo Page me hota hai?

    - (a) Total elements count
    - (b) Pagination
      ✅ Answer: (a)

19. Stream close karne ka best practice kya hai?

    - (a) Manually close karna
    - (b) Try-with-resources block
      ✅ Answer: (b)

20. Limit kaise apply karte ho method name me?
    - (a) ByOrder
    - (b) Top ya First
      ✅ Answer: (b)

### 📘 Real-World Use Cases

21. Jab 10,000 users ka data fetch karna ho to kya return type prefer karoge?
22. Agar result set small hai to List ka use safe hai ya nahi?
23. Asynchronous method call karke kya benefit hota hai?
24. Pageable aur Sort dono ek sath kaise manage karte hain?
25. List<User> vs Page<User> me performance difference kya hoga jab data bohot zyada ho?

## 📚 Final Summary

| Topic                              | Covered? |
| :--------------------------------- | :------- |
| Pageable, Slice, Sort parameters   | ✅       |
| Top, First keywords for limiting   | ✅       |
| Dynamic sorting (TypedSort, QSort) | ✅       |
| Special combinations rules         | ✅       |
| 30+ Practice Questions Ready       | ✅       |

## 📚 Quick Full 5-Part Notes Summary

### 🟠 Part-1: Query Method Basics + Lookup Strategies

- Spring Data JPA me query banane ke 2 tareeke: **method name** ya **@Query** manually.
- Query lookup strategies:
  - **CREATE:** Method name se query banana.
  - **USE_DECLARED_QUERY:** Sirf manually defined query dhoondhna.
  - **CREATE_IF_NOT_FOUND:** (Default) Pehle manually check, warna method name se banana.

### 🟠 Part-2: Query Creation Rules

- Query method me **Subject** aur **Predicate** hote hain.  
  (e.g., `findByLastname` → Subject: `find`, Predicate: `Lastname`)
- Use `And`, `Or`, `Between`, `LessThan`, `GreaterThan`, `Like` operators.
- Case ignore karne ke liye: `IgnoreCase` keyword.
- Sorting ke liye method me `OrderByPropertyAsc/Desc` likhte hain.

### 🟠 Part-3: Reserved Methods + Property Traversal

- Reserved methods jaise `findById()` **@Id** field pe hi kaam karte hain (even if field ka naam alag ho).
- Nested property access karne ke liye camel-case ya `_` (underscore) ka use karo.
- Underscore wale fields me double `_` ka use karna padta hai nested path ke liye.
- Confusion avoid karne ke liye \_ use karna important hai.

### 🟠 Part-4: Return Types (List, Stream, Streamable, Page, Slice)

- `List<T>`, `Iterable<T>`, `Set<T>`: Saare records ek baar me load.
- `Streamable<T>`: Iterable + functional features.
- `Stream<T>`: Record by record processing (must close).
- `Page<T>`: Full paging with total count.
- `Slice<T>`: Lightweight paging, no total count.

### 🟠 Part-5: Advanced Paging, Sorting, Limiting

- Pageable: dynamic paging (page number, size, sort).
- Slice: Sirf current data + next page info.
- Top/First: Fixed number of results (`Top5`, `First3` etc.)
- Pageable me alag se Sort/Limit nahi aa sakta.
- TypeSafe Sorting: `TypedSort`, `QSort` jaise APIs use kar sakte ho.

## 📈 Full Mindmap Diagram Overview

```plaintext
Defining Query Methods
│
├── 1. Query Lookup Strategies
│     ├── CREATE
│     ├── USE_DECLARED_QUERY
│     └── CREATE_IF_NOT_FOUND (default)
│
├── 2. Query Creation from Method Names
│     ├── Subject (find, exists)
│     ├── Predicate (ByLastname, ByAgeBetween)
│     ├── And / Or operators
│     ├── IgnoreCase, OrderBy
│
├── 3. Reserved Methods
│     ├── findById() → targets @Id property
│     ├── Special handling for id vs pk
│
├── 4. Property Traversal
│     ├── Nested property access
│     ├── Use of _ (underscore) to split
│
├── 5. Return Types
│     ├── List, Iterable, Set
│     ├── Streamable, Stream
│     ├── Page, Slice
│     ├── Async Future/CompletableFuture
│
├── 6. Paging, Sorting, Limiting
│     ├── Pageable, Sort parameters
│     ├── Limit using Top/First
│     ├── Special rules for combinations
│
└── Final Goal: Build flexible, optimized queries easily!
```

## ✏️ Mini Test Paper (30 Practice Questions)

### 📄 Section A: Short Answer (1-2 lines)

1. Spring Data JPA me query define karne ke 2 main tareeke kya hain?
2. Query lookup strategy me CREATE_IF_NOT_FOUND kya karta hai?
3. findByLastnameAndFirstname method me subject aur predicate kya hain?
4. Top keyword method me kya karta hai?
5. Slice aur Page me main difference kya hai?

### 📄 Section B: Code Writing

6. Aisa repository method likho jo `Page<User>` return kare lastname ke basis pe.
7. Method likho jo `findTop5ByAgeGreaterThan(int age)` type ka kaam kare.
8. Streamable type ka repository method example do.
9. Method likho jo nested property address.zipCode ko access kare.
10. Pageable object kaise create karte hain example ke saath batao.

### 📄 Section C: MCQ (Tick the correct option)

11. Pageable parameter ke saath Sort alag se pass kar sakte ho?

    - (a) Haan
    - (b) Nahi
      ✅ (b)

12. Slice result kis case me better hota hai?

    - (a) Jab total elements count chahiye
    - (b) Jab sirf next page ka check karna hai
      ✅ (b)

13. findById() kis field ko target karta hai?

    - (a) id field name
    - (b) @Id annotated field
      ✅ (b)

14. Stream result jab close nahi karte to kya problem hoti hai?

    - (a) No problem
    - (b) Memory leak / resource leak
      ✅ (b)

15. Top5 ka meaning kya hai?
    - (a) Sabhi laana
    - (b) 5 results laana
      ✅ (b)

### 📄 Section D: Real-World Scenarios

16. 1 million records hai, Page return karoge ya List? Kyun?
17. Nested address.zipCode ko safely access karna ho to kya karoge?
18. Kaunsa return type prefer karoge jab query slow database se aa raha ho?
19. Pageable unsorted banana ho to kya karoge?
20. Streamable kis situation me better hota hai compared to List?

## ✅ Final Deliverables Ready

| Material                       | Status |
| :----------------------------- | :----- |
| 5-Part Compact Notes           | ✅     |
| Mindmap Diagram                | ✅     |
| Mini Test Paper (30 Questions) | ✅     |

## 📚 Query Method Reference Table with Real Examples

### 🚀 Table: JPA Query Method Keywords + Method Example + Query + Real Data Fetch Example

| Keyword          | Method Example                                         | Query Example                                                       | Data Example Result (Vaccine Table)           |
| :--------------- | :----------------------------------------------------- | :------------------------------------------------------------------ | :-------------------------------------------- |
| **And**          | `findByCompanyAndPrice(String company, Integer price)` | `SELECT v FROM Vaccine v WHERE v.company = ?1 AND v.price = ?2`     | Bharat Biotech, 1200 ➔ Covaxin                |
| **Or**           | `findByCompanyOrPrice(String company, Integer price)`  | `SELECT v FROM Vaccine v WHERE v.company = ?1 OR v.price = ?2`      | Bharat Biotech ya price 1000                  |
| **IsNull**       | `findByCompanyIsNull()`                                | `SELECT v FROM Vaccine v WHERE v.company IS NULL`                   | (koi record nahi hoga unless NULL ho)         |
| **IsNotNull**    | `findByCompanyIsNotNull()`                             | `SELECT v FROM Vaccine v WHERE v.company IS NOT NULL`               | Sare vaccines                                 |
| **Between**      | `findByPriceBetween(Integer min, Integer max)`         | `SELECT v FROM Vaccine v WHERE v.price BETWEEN ?1 AND ?2`           | 1000-1500 ➔ Sputnik V, Moderna, Pfizer        |
| **LessThan**     | `findByPriceLessThan(Integer price)`                   | `SELECT v FROM Vaccine v WHERE v.price < ?1`                        | Price < 1000 ➔ Gamaleya Research, Cuba Center |
| **GreaterThan**  | `findByPriceGreaterThan(Integer price)`                | `SELECT v FROM Vaccine v WHERE v.price > ?1`                        | Price > 1300 ➔ Pfizer, Moderna, Sanofi-GSK    |
| **StartingWith** | `findByCompanyStartingWith(String prefix)`             | `SELECT v FROM Vaccine v WHERE v.company LIKE ?1%`                  | "Pfizer%" ➔ Pfizer-BioNTech                   |
| **EndingWith**   | `findByCompanyEndingWith(String suffix)`               | `SELECT v FROM Vaccine v WHERE v.company LIKE %?1`                  | "%Institute" ➔ VECTOR Institute               |
| **Containing**   | `findByCompanyContaining(String word)`                 | `SELECT v FROM Vaccine v WHERE v.company LIKE %?1%`                 | "Biotech" ➔ Bharat Biotech, Sinovac Biotech   |
| **OrderBy**      | `findByCompanyOrderByPriceAsc(String company)`         | `SELECT v FROM Vaccine v WHERE v.company = ?1 ORDER BY v.price ASC` | Bharat Biotech vaccines ordered by price      |
| **Not**          | `findByCompanyNot(String company)`                     | `SELECT v FROM Vaccine v WHERE v.company <> ?1`                     | Sare vaccines except Bharat Biotech           |
| **In**           | `findByCompanyIn(List<String> companies)`              | `SELECT v FROM Vaccine v WHERE v.company IN ?1`                     | [Pfizer-BioNTech, Moderna Inc.] vaccines      |
| **NotIn**        | `findByCompanyNotIn(List<String> companies)`           | `SELECT v FROM Vaccine v WHERE v.company NOT IN ?1`                 | Baaki sare vaccines                           |
| **True/False**   | (Boolean fields ke liye)                               | -                                                                   | Agar field like `isApproved` ho to            |
| **IgnoreCase**   | `findByCompanyIgnoreCase(String company)`              | `SELECT v FROM Vaccine v WHERE UPPER(v.company) = UPPER(?1)`        | "pfizer-biontech" bhi match karega            |

### 📈 Real-World Example Queries on Vaccine Data

#### 1. Bharat Biotech aur price 1200 ke basis pe vaccine dhoondhna

```java
List<Vaccine> findByCompanyAndPrice(String company, Integer price);
```

**Call:**

```java
findByCompanyAndPrice("Bharat Biotech", 1200)
```

**Result:** Covaxin

#### 2. Price between 1000 and 1500 vaccines

```java
List<Vaccine> findByPriceBetween(Integer start, Integer end);
```

**Call:**

```java
findByPriceBetween(1000, 1500)
```

**Result:**

- Sputnik V (1000)
- Moderna (1500)
- Pfizer (1800 ❌ too high)
- Covovax (1150)

#### 3. Company name containing "Biotech"

```java
List<Vaccine> findByCompanyContaining(String keyword);
```

**Call:**

```java
findByCompanyContaining("Biotech")
```

**Result:**

- Bharat Biotech
- Sinovac Biotech

#### 4. Vaccines sorted by price ascending for company 'Novavax'

```java
List<Vaccine> findByCompanyOrderByPriceAsc(String company);
```

**Call:**

```java
findByCompanyOrderByPriceAsc("Novavax")
```

**Result:**

- Novavax, Nuvaxovid

#### 5. Vaccines where company ends with "Institute"

```java
List<Vaccine> findByCompanyEndingWith(String suffix);
```

**Call:**

```java
findByCompanyEndingWith("Institute")
```

**Result:**

- VECTOR Institute
- Cuba Finlay Institute

### 📋 Practice Questions (Vaccine Data Based)

#### 📘 Basic Concept

1. `findByPriceLessThan(1000)` kya fetch karega?
2. `findByPriceGreaterThan(1200)` ka kya result ayega?
3. `findByCompanyStartingWith("Sinovac")` kya dega?
4. `findByCompanyEndingWith("Institute")` kya laega?
5. `findByCompanyContaining("National")` kya return karega?

#### 📘 Coding Practice

6. Method likho jo company name aur price dono ke basis pe vaccine dhoondhe.
7. Method likho jo price between 900 and 1200 range ka vaccine fetch kare.
8. Method likho jo vaccines ko company ke naam ke ascending order me laaye.
9. Method likho jo "Biotech" word ke basis pe vaccines fetch kare.
10. Method likho jo company not equal to "Pfizer" wali vaccines dhoonde.

#### 📘 MCQ

11. findByCompanyIgnoreCase("pfizer-biontech") kya karega?

    - (a) Fail hoga
    - (b) Case-insensitive match karega
      ✅ (b)

12. findByPriceIn([800, 1200, 1500]) kya karega?

    - (a) 3 prices ka match karega
    - (b) Sirf ek match karega
      ✅ (a)

13. EndingWith keyword kis pattern me query banata hai?

    - (a) value%
    - (b) %value
      ✅ (b)

14. @Query likhne par automatic method name parsing hoti hai kya?

    - (a) Haan
    - (b) Nahi
      ✅ (b)

15. Containing keyword ka LIKE pattern kya hota hai?
    - (a) value%
    - (b) %value%
      ✅ (b)

#### 📘 Real-Life Scenarios

16. Vaccine name containing "covid" ko kaise search karoge?
17. Company name ke hisaab se sabse sasti vaccine kaise laoge?
18. Price greater than 1300 ka ascending order me vaccines kaise fetch karoge?
19. "Biotech" aur "Institute" dono wale vaccines fetch karne ke liye method likho.
20. Top 5 cheapest vaccines kaise fetch karoge?

#### 📘 Bonus Hard

21. Offset scrolling ke use case vaccine search me kya ho sakte hain?
22. Keyset scrolling aur offset scrolling me difference kya hai?
23. LIKE query me escape kaise karte hain agar user input dangerous hai?
24. Query hint lagake readOnly vaccine query kaise banate hain?
25. Multiple filters (Company + Price) lagake query kaise define karoge?

#### 📘 Final Few Conceptual

26. Derived delete query kya hota hai?
27. Modifying query me auto clear karna kab zaruri hota hai?
28. Native query me SQL injection se kaise bachte hain?
29. NamedQuery aur @Query me kya difference hai?
30. Scrolling query me window size ka kya impact hota hai?

## ✅ Final Deliverables Ready

| Item                            | Status |
| :------------------------------ | :----- |
| Full Table + Examples           | ✅     |
| Vaccine Real Data Based Queries | ✅     |
| 30 Practice Questions           | ✅     |

## 📊 Vaccine Data Query Examples

### ✅ Step-1: Vaccine Table (Original Data)

| id  | company               | price | vaccine_name    |
| --- | --------------------- | ----- | --------------- |
| 252 | Bharat Biotech        | 1200  | Covaxin         |
| 253 | AstraZeneca           | 800   | Covishield      |
| 254 | Gamaleya Research     | 1000  | Sputnik V       |
| 255 | Moderna Inc.          | 1500  | Moderna         |
| 256 | Pfizer-BioNTech       | 1800  | Pfizer          |
| 257 | Sinovac Biotech       | 1100  | Sinovac         |
| 258 | China National        | 1050  | Sinopharm       |
| 259 | Johnson & Johnson     | 1400  | Janssen         |
| 260 | Novavax Inc.          | 1300  | Novavax         |
| 261 | CanSino Biologics     | 950   | CanSino         |
| 262 | VECTOR Institute      | 900   | EpiVacCorona    |
| 263 | Serum Institute       | 1150  | Covovax         |
| 264 | Zydus Cadila          | 1250  | ZyCoV-D         |
| 265 | Cuba Center           | 950   | Abdala          |
| 266 | Cuba Finlay Institute | 970   | Soberana 02     |
| 267 | Sinopharm             | 1020  | BBIBP-CorV      |
| 268 | Biological E Ltd.     | 850   | Corbevax        |
| 269 | Novavax               | 1350  | Nuvaxovid       |
| 270 | Sanofi-GSK            | 1450  | VidPrevtyn Beta |
| 271 | Kazakhstan Research   | 800   | QazVac          |

### ✅ Step-2: Method Table (Which Method Use → Kya Milega)

| Keyword      | Method Example                                         | Matlab kya hai?                                   |
| :----------- | :----------------------------------------------------- | :------------------------------------------------ |
| And          | `findByCompanyAndPrice("Bharat Biotech", 1200)`        | Bharat Biotech aur price 1200 wala vaccine        |
| Or           | `findByCompanyOrPrice("Novavax", 1300)`                | Company Novavax ya Price 1300 match               |
| LessThan     | `findByPriceLessThan(1000)`                            | Price 1000 se kam wale vaccines                   |
| GreaterThan  | `findByPriceGreaterThan(1300)`                         | Price 1300 se jyada wale vaccines                 |
| Between      | `findByPriceBetween(900, 1200)`                        | Price 900 se 1200 ke beech wale vaccines          |
| StartingWith | `findByCompanyStartingWith("Cuba")`                    | Company name Cuba se start hone wale              |
| EndingWith   | `findByCompanyEndingWith("Institute")`                 | Company name Institute pe end hone wale           |
| Containing   | `findByCompanyContaining("Biotech")`                   | Company name me Biotech word hone wale            |
| OrderBy      | `findByCompanyOrderByPriceAsc("Novavax")`              | Novavax company ke vaccines ko price ascending me |
| Not          | `findByCompanyNot("Pfizer-BioNTech")`                  | Sare vaccines except Pfizer                       |
| In           | `findByCompanyIn(["Moderna Inc.", "Pfizer-BioNTech"])` | Moderna, Pfizer                                   |
| IgnoreCase   | `findByCompanyIgnoreCase("pfizer-biontech")`           | Pfizer                                            |

### ✅ Step-3: Find karke Real Result Table (Direct Output)

| Method Example                                         | Result                                                                                        |
| :----------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
| `findByCompanyAndPrice("Bharat Biotech", 1200)`        | Covaxin                                                                                       |
| `findByPriceLessThan(1000)`                            | Covishield, Sputnik V, EpiVacCorona, CanSino, Abdala, Cuba Finlay Institute, Corbevax, QazVac |
| `findByPriceGreaterThan(1300)`                         | Pfizer, Janssen, Novavax, VidPrevtyn Beta                                                     |
| `findByPriceBetween(900, 1200)`                        | Sputnik V, Sinovac, Sinopharm, EpiVacCorona, Covovax                                          |
| `findByCompanyStartingWith("Cuba")`                    | Abdala, Soberana 02                                                                           |
| `findByCompanyEndingWith("Institute")`                 | VECTOR Institute, Cuba Finlay Institute, Serum Institute                                      |
| `findByCompanyContaining("Biotech")`                   | Bharat Biotech, Sinovac Biotech                                                               |
| `findByCompanyOrderByPriceAsc("Novavax")`              | Novavax, Nuvaxovid                                                                            |
| `findByCompanyNot("Pfizer-BioNTech")`                  | All except Pfizer                                                                             |
| `findByCompanyIn(["Moderna Inc.", "Pfizer-BioNTech"])` | Moderna, Pfizer                                                                               |
| `findByCompanyIgnoreCase("pfizer-biontech")`           | Pfizer                                                                                        |

### ✅ Summary

| Table   | Kya diya gaya?                       |
| :------ | :----------------------------------- |
| Table-1 | Clean Vaccine Data                   |
| Table-2 | Method ka use aur kya karega         |
| Table-3 | Actual findBy queries ka real output |

## 📚 Chapter 4: Projections - Full Simple Notes + Example

### 4.1 Projections Kya Hota Hai?

**Simple:**

- Normally jab query chalti hai, pura entity (full object) fetch hota hai.
- **Projection** ka matlab hota hai:  
  ➔ **Sirf kuch fields fetch karna**, na ki poora object.
- **Performance fast hoti hai** aur **memory bachti hai**.

### 4.2 Basic Example

Entity:

```java
class Person {
    UUID id;
    String firstname;
    String lastname;
    Address address;
}
class Address {
    String zipCode;
    String city;
    String street;
}
```

Repository:

```java
interface PersonRepository extends Repository<Person, UUID> {
    Collection<Person> findByLastname(String lastname);
}
```

🔴 Problem: Poora Person object aayega, but mujhe sirf firstname + lastname chahiye.

✅ Solution: **Projections**

### 4.3 Types of Projections

| Type                     | Example                                                 | Notes                |
| :----------------------- | :------------------------------------------------------ | :------------------- |
| Interface-based          | `interface NamesOnly`                                   | Best: Simple         |
| Class-based (DTOs)       | `record NamesOnly(...)`                                 | Good for performance |
| Open Projection (@Value) | `@Value("#{target.firstname + ' ' + target.lastname}")` | Customize value      |
| Dynamic Projection       | `<T> Collection<T> findByLastname(...)`                 | Decide at runtime    |
| Nested Projections       | `interface AddressSummary` inside `PersonSummary`       | Fetch nested fields  |

### 4.4 Interface-Based Projection

```java
interface NamesOnly {
    String getFirstname();
    String getLastname();
}
```

Repository:

```java
interface PersonRepository extends Repository<Person, UUID> {
    Collection<NamesOnly> findByLastname(String lastname);
}
```

✅ Sirf firstname, lastname return honge, **poora Person object nahi**.

### 4.5 Nested Interface Projection

```java
interface PersonSummary {
    String getFirstname();
    String getLastname();
    AddressSummary getAddress();

    interface AddressSummary {
        String getCity();
    }
}
```

✅ Yahan `PersonSummary` ke andar `AddressSummary` hai. Address ka sirf city milega.

### 4.6 Closed vs Open Projection

| Type              | Meaning                             | Example                                                 |
| :---------------- | :---------------------------------- | :------------------------------------------------------ |
| Closed Projection | Fields exactly match entity fields. | `String getFirstname()`                                 |
| Open Projection   | Fields dynamically bante hain.      | `@Value("#{target.firstname + ' ' + target.lastname}")` |

### 4.7 Open Projection Example (@Value)

```java
interface NamesOnly {
    @Value("#{target.firstname + ' ' + target.lastname}")
    String getFullName();
}
```

✅ Yeh **dynamic string** banayega:  
Example → "Ravi Kumar"

### 4.8 Default Method in Projection (Java 8+)

```java
interface NamesOnly {
    String getFirstname();
    String getLastname();

    default String getFullName() {
        return getFirstname() + " " + getLastname();
    }
}
```

✅ Without @Value, hum apne method se bana sakte hain.

### 4.9 Spring Bean call inside Projection (@Value se)

Bean:

```java
@Component
class MyBean {
    String getFullName(Person person) {
        return person.getFirstname() + " " + person.getLastname();
    }
}
```

Projection:

```java
interface NamesOnly {
    @Value("#{@myBean.getFullName(target)}")
    String getFullName();
}
```

✅ Bean ke method ko call karke projection ka field ban raha hai.

### 4.10 Nullable Wrapper Projection

```java
interface NamesOnly {
    Optional<String> getFirstname();
}
```

✅ Agar firstname null hoga, to `Optional.empty()` milega.  
Supported types: `Optional`, `Vavr Option`, `Scala Option`, etc.

### 4.11 Class-Based (DTO) Projection (Record Based)

```java
record NamesOnly(String firstname, String lastname) {}
```

Repository:

```java
interface PersonRepository extends Repository<Person, UUID> {
    Collection<NamesOnly> findByLastname(String lastname);
}
```

✅ **No proxy**, direct DTO object aata hai, memory optimized.

### 4.12 Quick Table Summary (Easy Learning)

| Feature                     | Interface Projection               | DTO Projection (Record)        |
| :-------------------------- | :--------------------------------- | :----------------------------- |
| How it works                | Proxy banake getter call karta hai | Direct object create karta hai |
| Supports nested projection? | Yes                                | No                             |
| Performance                 | Medium                             | High                           |
| Complexity                  | Less                               | Less                           |

### 4.13 Dynamic Projections

Method:

```java
<T> Collection<T> findByLastname(String lastname, Class<T> type);
```

Call Examples:

```java
Collection<Person> allPersons = repo.findByLastname("Sharma", Person.class);
Collection<NamesOnly> onlyNames = repo.findByLastname("Sharma", NamesOnly.class);
```

✅ Runtime par decide kar sakte ho ki **full entity chahiye ya sirf projection**.

### 4.14 Special in JPA

| Query Type    | Notes                                                |
| :------------ | :--------------------------------------------------- |
| Derived Query | Auto projection support                              |
| JPQL with DTO | Must use `SELECT new com.example.DTO(f1, f2)` syntax |
| Native Query  | Use mapping or direct DTO constructor                |

### 4.15 Real Life Example Table (Projection Output)

| Query                      | Projection Interface                                  | Output                            |
| :------------------------- | :---------------------------------------------------- | :-------------------------------- |
| `findByLastname("Sharma")` | `NamesOnly`                                           | Only firstname, lastname          |
| `findByLastname("Sharma")` | `PersonSummary`                                       | firstname, lastname, address.city |
| `findByLastname("Sharma")` | `record NamesOnly(String firstname, String lastname)` | DTO objects                       |

### 4.16 Practice Questions

1. Projection kya hota hai?
2. Closed projection aur open projection ka kya difference hai?
3. Nested projections kaise likhte hain?
4. Interface-based projections me proxy banta hai ya real object?
5. DTO projection me proxy banta hai kya?
6. Dynamic projection ka use case kya hai?
7. @Value kahan use karte hain projections me?
8. Optional ka use projection me kaise hota hai?
9. Projection me Spring Bean ka method call kaise karte hain?
10. DTO class me kaunsa constructor hona zaruri hai?
11. JPQL me DTO kaise return karte hain?
12. Native query me projection kaise use karte hain?
13. Projection field null ho to kya return hoga?
14. Dynamic projection kaise call karte hain method se?
15. Projection me address ka sirf city field kaise fetch karoge?
16. DTO me nested projection allowed hai kya?
17. @PersistenceCreator annotation kab use karte hain?
18. Record class projection ke kya advantage hain?
19. Projection ke saath count query kaise optimize hota hai?
20. Projection ke saath complex aggregation query kaise likhte hain?

### 4.17 Chapter Summary

| Step                            | Status |
| :------------------------------ | :----- |
| Full Concept Clear kar diya     | ✅     |
| Real Code Examples diye         | ✅     |
| Quick Tables and Shortcuts diye | ✅     |
| Practice Questions diye         | ✅     |

## 📚 Chapter 5: Dynamic Projections - Live Example

### 5.1 Dynamic Projection Kya Hota Hai?

**Simple:**

- Runtime pe decide kar sakte ho ki **kaunsa projection use karna hai**
- Ek hi method se multiple types ke projections fetch kar sakte ho
- Type safety maintain hoti hai

### 5.2 Live Example with "Vani Priya" and "Ravi Kumar"

#### 5.2.1 Repository Method

```java
@Repository
public interface PersonRepository extends JpaRepository<Person, Long> {

    // Dynamic Projection Method
    <T> List<T> findByLastname(String lastname, Class<T> type);
}
```

#### 5.2.2 Different Projection Types

```java
// 1. Simple Names Projection
public interface NamesOnly {
    String getFirstname();
    String getLastname();
}

// 2. Full Name Projection
public interface FullNameOnly {
    @Value("#{target.firstname + ' ' + target.lastname}")
    String getFullName();
}

// 3. Address Summary Projection
public interface AddressSummary {
    String getCity();
    String getZipCode();
}

// 4. Complete Person Summary
public interface PersonSummary {
    String getFirstname();
    String getLastname();
    AddressSummary getAddress();
}
```

#### 5.2.3 Service Layer Example

```java
@Service
public class PersonService {

    @Autowired
    private PersonRepository personRepository;

    // 1. Fetch Only Names
    public List<NamesOnly> getNamesOnly(String lastname) {
        return personRepository.findByLastname(lastname, NamesOnly.class);
    }

    // 2. Fetch Full Names
    public List<FullNameOnly> getFullNames(String lastname) {
        return personRepository.findByLastname(lastname, FullNameOnly.class);
    }

    // 3. Fetch Person Summary
    public List<PersonSummary> getPersonSummary(String lastname) {
        return personRepository.findByLastname(lastname, PersonSummary.class);
    }
}
```

#### 5.2.4 Controller Example

```java
@RestController
@RequestMapping("/api/persons")
public class PersonController {

    @Autowired
    private PersonService personService;

    // 1. Get Names Only
    @GetMapping("/names/{lastname}")
    public List<NamesOnly> getNames(@PathVariable String lastname) {
        return personService.getNamesOnly(lastname);
    }

    // 2. Get Full Names
    @GetMapping("/fullnames/{lastname}")
    public List<FullNameOnly> getFullNames(@PathVariable String lastname) {
        return personService.getFullNames(lastname);
    }

    // 3. Get Person Summary
    @GetMapping("/summary/{lastname}")
    public List<PersonSummary> getSummary(@PathVariable String lastname) {
        return personService.getPersonSummary(lastname);
    }
}
```

### 5.3 Live Output Examples

#### 5.3.1 NamesOnly Projection (GET /api/persons/names/Priya)

```json
[
  {
    "firstname": "Vani",
    "lastname": "Priya"
  }
]
```

#### 5.3.2 FullNameOnly Projection (GET /api/persons/fullnames/Priya)

```json
[
  {
    "fullName": "Vani Priya"
  }
]
```

#### 5.3.3 PersonSummary Projection (GET /api/persons/summary/Priya)

```json
[
  {
    "firstname": "Vani",
    "lastname": "Priya",
    "address": {
      "city": "Mumbai",
      "zipCode": "400001"
    }
  }
]
```

### 5.4 Quick Reference Table

| Projection Type | API Endpoint                 | Example Output               |
| :-------------- | :--------------------------- | :--------------------------- |
| NamesOnly       | /api/persons/names/Priya     | firstname, lastname          |
| FullNameOnly    | /api/persons/fullnames/Priya | fullName                     |
| PersonSummary   | /api/persons/summary/Priya   | firstname, lastname, address |

### 5.5 Practice Questions

1. Dynamic projection ka main advantage kya hai?
2. Runtime pe projection type change karne ke liye kya karna padta hai?
3. Dynamic projection me type safety kaise maintain hoti hai?
4. Multiple projection types ek sath kaise handle kar sakte hain?
5. Dynamic projection me performance ka kya impact hota hai?

### 5.6 Chapter Summary

| Step                             | Status |
| :------------------------------- | :----- |
| Dynamic Projection Concept Clear | ✅     |
| Live Code Examples diye          | ✅     |
| API Endpoints dikhaye            | ✅     |
| JSON Output Examples diye        | ✅     |
| Practice Questions diye          | ✅     |

## 📘 Chapter: Stored Procedures in JPA (Book-Style Hindi Mein)

### 🔹 Stored Procedure kya hota hai?

Stored Procedure ek pre-written SQL function hota hai jo database ke andar save rehta hai. Jab bhi aapko complex logic ya repetitive query chalani ho — toh aap sirf procedure ka naam call karke kaam kar sakte ho.

### 🔹 JPA ke through Stored Procedure ka use kaise hota hai?

JPA 2.1 se `@Procedure` aur `@NamedStoredProcedureQuery` ke madhyam se stored procedures ko Java code se call kar sakte ho — bina JDBC boilerplate code likhe.

### ✅ Step 1: SQL Stored Procedure likhna

```sql
-- agar pehle se hai toh hata do
DROP PROCEDURE IF EXISTS plus1inout;

-- procedure banayein
CREATE PROCEDURE plus1inout(IN arg INT, OUT res INT)
BEGIN
  SET res = arg + 1;
END;
```

☝️ Iska matlab hai: jo bhi number `arg` mein doge, woh 1 add karke `res` mein milega.

### ✅ Step 2: JPA Entity mein Metadata dena

```java
@Entity
@NamedStoredProcedureQuery(
  name = "User.plus1",
  procedureName = "plus1inout",
  parameters = {
    @StoredProcedureParameter(mode = ParameterMode.IN, name = "arg", type = Integer.class),
    @StoredProcedureParameter(mode = ParameterMode.OUT, name = "res", type = Integer.class)
  }
)
public class User {
  @Id
  private Long id;
}
```

📌 `name`: JPA ke andar stored procedure ka naam  
📌 `procedureName`: Actual DB stored procedure ka naam  
📌 `parameters`: procedure ke inputs/outputs

### ✅ Step 3: Repository Method banana

```java
public interface UserRepository extends JpaRepository<User, Long> {

  @Procedure(name = "User.plus1")
  Integer plus1inout(@Param("arg") Integer arg);
}
```

☝️ Is method ko call karoge to database procedure run karega aur `arg + 1` return karega.

## 🧩 Multiple OUT Parameters Example

### ✅ SQL Procedure:

```sql
CREATE PROCEDURE multi_out(IN input INT, OUT doubled INT, OUT message VARCHAR(100))
BEGIN
  SET doubled = input * 2;
  SET message = 'Success';
END;
```

### ✅ Entity Configuration:

```java
@NamedStoredProcedureQuery(
  name = "User.multi_out",
  procedureName = "multi_out",
  parameters = {
    @StoredProcedureParameter(mode = ParameterMode.IN, name = "input", type = Integer.class),
    @StoredProcedureParameter(mode = ParameterMode.OUT, name = "doubled", type = Integer.class),
    @StoredProcedureParameter(mode = ParameterMode.OUT, name = "message", type = String.class)
  }
)
```

### ✅ Repository Method:

```java
@Procedure(name = "User.multi_out")
Map<String, Object> getMultiOutput(@Param("input") Integer input);
```

Output:

```json
{
  "doubled": 20,
  "message": "Success"
}
```

## 📊 ParameterMode Meaning

| ParameterMode | Explanation (Hindi mein)              |
| ------------- | ------------------------------------- |
| IN            | Java se value DB ko bhejna            |
| OUT           | DB se value Java mein laana           |
| INOUT         | Dono direction mein value ka flow     |
| REF_CURSOR    | Cursor result return (PostgreSQL etc) |

## 📘 Interview ke liye 20 Questions + Answers Table

| No. | Question                                                          | Answer                                                          |
| --- | ----------------------------------------------------------------- | --------------------------------------------------------------- |
| 1   | Stored Procedure kya hota hai?                                    | Predefined SQL code jo DB mein store hota hai.                  |
| 2   | JPA mein procedure metadata kaunsi annotation se banti hai?       | `@NamedStoredProcedureQuery`                                    |
| 3   | Repository method pe procedure kaise call karte hain?             | `@Procedure` annotation se                                      |
| 4   | ParameterMode.IN ka matlab?                                       | Java se input parameter bhejna                                  |
| 5   | ParameterMode.OUT ka matlab?                                      | Database se output parameter lena                               |
| 6   | Agar 1 output ho toh return type kya hoga?                        | Integer, String etc.                                            |
| 7   | Agar multiple OUT parameters ho to return type kya hoga?          | `Map<String, Object>`                                           |
| 8   | Kya procedure se ResultSet return ho sakta hai?                   | Haan, REF_CURSESTOR se                                          |
| 9   | `procedureName` aur `name` mein farak?                            | `procedureName` DB ka naam, `name` JPA ka naam hota hai         |
| 10  | Agar method name same ho toh `@Procedure` mein kya likhna padega? | Kuch nahi likhna padta, method name se match ho jaata hai       |
| 11  | Procedure ka output agar optional ho to kya karein?               | OUT parameter use karo                                          |
| 12  | @Param ka kya use hai?                                            | Method argument ko procedure ke parameter se bind karna         |
| 13  | Multiple OUT values kaise receive karte hain?                     | `Map<String, Object>` return karke                              |
| 14  | Agar koi value return nahi hoti ho to method ka return kya ho?    | `void`                                                          |
| 15  | Procedure testing ke liye kaunsa database use ho sakta hai?       | H2 in-memory DB ya MySQL                                        |
| 16  | Kya procedure DTO return kar sakta hai?                           | Advanced mapping ke sath haan, @SqlResultSetMapping se          |
| 17  | Procedure ke saath SpEL ya Expression chalega kya?                | Nahi, procedure static hote hain                                |
| 18  | Kya `@Procedure` @Transactional hona chahiye?                     | Haan, agar data update/delete ho raha ho                        |
| 19  | Spring Boot mein procedure ka configuration kaise hota hai?       | Entity class par annotation aur repository par method           |
| 20  | Agar method aur procedure name match nahi karein to?              | `@Procedure(name="...")` ya `procedureName="..."` likhna padega |

## ✅ Summary

- Use `@NamedStoredProcedureQuery` in Entity
- Use `@Procedure` in Repository
- Use `Map<String, Object>` for multiple OUT
- Test with H2 DB or MySQL
- Procedure ka naam aur method ka naam alag ho sakta hai

## 📘 Chapter: Specifications in Spring Data JPA (Book-Style Hindi Mein)

### 🔹 Step 1: SQL Table Example

Hum ek customer table assume karte hain:

📋 SQL Table: customer
| id | name | created_at | total_purchase |
|----|-------------|-------------|----------------|
| 1 | Ravi Kumar | 2020-01-15 | 500.00 |
| 2 | Vani Priya | 2023-03-10 | 100.00 |
| 3 | Arjun Verma | 2018-09-20 | 1200.00 |
| 4 | Neha Sharma | 2022-08-01 | 150.00 |

🧠 Ab Requirement
Humko chahiye:

- Wo customers jo 2 saal se purane hain (long-term)
- Ya jinki total_purchase > 200 ho

### 🔹 Step 2: Entity Class

```java
@Entity
public class Customer {

  @Id
  private Long id;

  private String name;

  private LocalDate createdAt;

  private BigDecimal totalPurchase;

  // getters-setters
}
```

### 🔹 Step 3: Repository

```java
public interface CustomerRepository extends
    JpaRepository<Customer, Long>,
    JpaSpecificationExecutor<Customer> {
}
```

### 🔹 Step 4: Specification Class

```java
public class CustomerSpecs {

  // 1. Long-term customer: createdAt < today - 2 years
  public static Specification<Customer> isLongTermCustomer() {
    return (root, query, builder) -> {
      LocalDate date = LocalDate.now().minusYears(2);
      return builder.lessThan(root.get("createdAt"), date);
    };
  }

  // 2. Total purchase > 200
  public static Specification<Customer> hasSalesOfMoreThan(BigDecimal value) {
    return (root, query, builder) ->
      builder.greaterThan(root.get("totalPurchase"), value);
  }
}
```

### 🔹 Step 5: Use Case in Service

```java
@Autowired
CustomerRepository customerRepository;

public List<Customer> getFilteredCustomers() {
  BigDecimal amount = new BigDecimal("200.00");

  return customerRepository.findAll(
      CustomerSpecs.isLongTermCustomer()
      .or(CustomerSpecs.hasSalesOfMoreThan(amount))
  );
}
```

### 💥 Real SQL Query Generated (approximate)

```sql
SELECT * FROM customer
WHERE created_at < '2023-05-01' OR total_purchase > 200.00;
```

### 🔹 Step 6: Delete Example

```java
Specification<Customer> deleteUnder18 = (root, query, cb) ->
    cb.lessThan(root.get("age").as(Integer.class), 18);

customerRepository.delete(deleteUnder18);
```

⚠️ Note: This works only in Spring Data JPA with JPA 2.1+, and returns number of rows deleted.

### 📘 Summary Table

| Concept                  | Meaning (Hindi Mein)                                        |
| ------------------------ | ----------------------------------------------------------- |
| Specification            | Ek programmatic condition jo query banata hai               |
| CriteriaBuilder          | JPA ka query builder                                        |
| Predicate                | WHERE clause ka logical expression                          |
| JpaSpecificationExecutor | Repository interface jo specifications ko support karta hai |
| toPredicate              | Method jisme criteria banate hain                           |
| findAll(Specification)   | Sab matching results laata hai                              |
| delete(Specification)    | JPA 2.1 mein matching data delete kar deta hai              |

### ❓ Interview Practice Questions

1. Specification kya hota hai Spring Data JPA mein?
2. toPredicate method ka kya kaam hota hai?
3. CriteriaBuilder aur Predicate ka relation kya hai?
4. Specification pattern ka fayda kya hai compared to @Query?
5. delete(Specification) method kab se available hai?
6. CriteriaBuilder.lessThan() ka kya use hai?
7. Specification objects ko kaise chain karte ho?
8. .or(...), .and(...) specification methods kya karte hain?
9. Specification ke bina where clause kaise likhte ho?
10. CriteriaBuilder.greaterThan() kis datatype ke liye use karte ho?

## 🔷 Query by Example (QBE) kya hota hai?

QBE ek simple tarika hai query likhne ka jisme hume field name ya SQL likhne ki jarurat nahi padti.

**Bas ek object banao** jisme jo values match karni hai wo fill karo — baaki Spring Data JPA khud se query bana lega.

## 🔷 Chaaro main part hota hai QBE ke:

| Part                        | Kya karta hai                                                     |
| --------------------------- | ----------------------------------------------------------------- |
| **1. Probe**                | Ek domain object jisme matching value daali jaati hai             |
| **2. ExampleMatcher**       | Batata hai kaise match karna hai (like endsWith, ignoreCase etc.) |
| **3. Example**              | Probe + Matcher milke banta hai Example                           |
| **4. FetchableFluentQuery** | Aur control deta hai jaise sort, project, pagination              |

## 🔷 Ek table leke samjho (SQL Table):

```sql
CREATE TABLE person (
  id VARCHAR PRIMARY KEY,
  firstname VARCHAR,
  lastname VARCHAR,
  city VARCHAR
);
```

| id  | firstname | lastname | city   |
| --- | --------- | -------- | ------ |
| 1   | Ravi      | Kumar    | Delhi  |
| 2   | Vani      | Priya    | Mumbai |
| 3   | Raj       | Malhotra | Delhi  |
| 4   | Vani      | Singh    | Patna  |

## 🔷 Java Entity Class:

```java
@Entity
public class Person {
  @Id
  private String id;
  private String firstname;
  private String lastname;
  private String city;
}
```

## 🔷 Step-by-step QBE

### 🟢 Step 1: Probe object banao

```java
Person probe = new Person();
probe.setFirstname("Vani");
```

### 🟢 Step 2: Example banao

```java
Example<Person> example = Example.of(probe);
```

### 🟢 Step 3: Query chalao

```java
List<Person> list = personRepository.findAll(example);
```

📌 Ye query SQL me convert hoga:

```sql
SELECT * FROM person WHERE firstname = 'Vani';
```

## 🔷 ExampleMatcher ka use:

```java
ExampleMatcher matcher = ExampleMatcher.matching()
  .withIgnorePaths("lastname")
  .withStringMatcher(StringMatcher.CONTAINING)
  .withIgnoreCase();
```

📌 isse ye query milegi:

```sql
SELECT * FROM person WHERE LOWER(firstname) LIKE '%vani%';
```

## 🔷 Fluent API ka use:

```java
Optional<Person> result = personRepository.findBy(
  example,
  q -> q.sortBy(Sort.by("lastname").descending()).first()
);
```

## 🔷 Matching Options Table (Important):

| Matcher      | Query Result SQL Like |
| ------------ | --------------------- |
| DEFAULT      | firstname = ?         |
| EXACT        | firstname = ?         |
| STARTING     | firstname LIKE ?%     |
| ENDING       | firstname LIKE %?     |
| CONTAINING   | firstname LIKE %?%    |
| + IgnoreCase | LOWER(fname) used     |

## 🔷 20 Questions for Practice (Book-style)

| #   | Question                                           |
| --- | -------------------------------------------------- |
| 1   | QBE kya hota hai?                                  |
| 2   | Probe object kisliye banate hain?                  |
| 3   | Example aur ExampleMatcher ka kya role hai?        |
| 4   | findAll(Example.of(probe)) kya karta hai?          |
| 5   | ExampleMatcher.matchingAny() ka matlab?            |
| 6   | withIgnorePaths("city") ka use kya hai?            |
| 7   | CONTAINING match ka output kya hoga?               |
| 8   | IgnoreCase lagane ka fayda kya hai?                |
| 9   | fetchableFluentQuery kyu use karte hain?           |
| 10  | findBy(...) ke 2nd parameter ka use?               |
| 11  | Kaise multiple properties match karte ho?          |
| 12  | QBE me nested object match hota hai kya?           |
| 13  | Regex QBE me supported hai ya nahi?                |
| 14  | Default matcher behaviour kya hai?                 |
| 15  | QBE me pagination kaise karte ho?                  |
| 16  | startsWith() aur endsWith() me difference?         |
| 17  | ExampleMatcher me ignoreNullValue ka kya use hai?  |
| 18  | FluentQuery ke first() aur one() ka farq?          |
| 19  | QBE kis case me fail hota hai?                     |
| 20  | QBE vs normal JPQL: kab kaun use karna better hai? |

## 🔷 Transactionality in Spring Data JPA - Complete Guide

### 🤔 What is Transactionality?

When we perform any database operations (read/write/update/delete), they should be wrapped in a **transaction** to maintain data **consistency**.

In Spring Data JPA, we use the `@Transactional` annotation to manage transactions.

## 🔹 Default Transaction Configuration

| Method Type                | Default Transaction Config        |
| -------------------------- | --------------------------------- |
| findById(), findAll()      | `@Transactional(readOnly = true)` |
| save(), delete(), update() | `@Transactional` (no readOnly)    |

This default configuration is inherited from **SimpleJpaRepository**.

## 🔷 Example Table (User Table)

```sql
CREATE TABLE users (
  id BIGINT PRIMARY KEY,
  name VARCHAR(100),
  active BOOLEAN
);
```

## 📚 Transactionality in Spring Data JPA - 20 Questions with Answers

### 1. Transaction kya hota hai Spring Data JPA mein?

Transaction ek atomic unit of work hota hai jisme multiple database operations ek sath execute hote hain. Agar koi bhi operation fail hota hai, to saare operations rollback ho jaate hain. Transaction ka main purpose data consistency maintain karna hota hai.

### 2. @Transactional annotation ka kya use hota hai?

@Transactional annotation Spring ko batata hai ki ye method transaction ke andar execute hona chahiye. Ye annotation method ya class level pe lagaya ja sakta hai. Iske through hum transaction management ko declarative way mein handle kar sakte hain.

### 3. Transaction ke main properties kya hote hain?

Transaction ke 4 main properties hote hain (ACID):

- Atomicity: Ya to saare operations success honge ya koi nahi
- Consistency: Database ek valid state se dusre valid state mein jaayega
- Isolation: Concurrent transactions ek dusre ko affect nahi karenge
- Durability: Once committed, changes permanent hote hain

### 4. Transaction propagation kya hota hai?

Transaction propagation batata hai ki agar ek transaction already chal raha hai, to naya transaction kaise behave karega. Kuch common propagation types:

- REQUIRED (default): Existing transaction use karega, nahi to naya banayega
- REQUIRES_NEW: Hamesha naya transaction banayega
- NESTED: Existing transaction ke andar nested transaction banayega
- SUPPORTS: Existing transaction use karega, nahi to transaction ke bina chalega

### 5. Transaction isolation level kya hota hai?

Isolation level batata hai ki ek transaction dusre concurrent transactions se kitna isolated hai. Common levels:

- READ_UNCOMMITTED: Sabse kam isolation
- READ_COMMITTED: Default level
- REPEATABLE_READ: Higher isolation
- SERIALIZABLE: Sabse zyada isolation

### 6. @Transactional mein timeout kaise set karte hain?

Timeout set karne ke liye @Transactional annotation mein timeout property use karte hain:

```java
@Transactional(timeout = 30) // 30 seconds
public void someMethod() {
    // method code
}
```

### 7. Transaction rollback kaise hota hai?

Transaction automatically rollback ho jata hai agar:

- Runtime exception aati hai
- Error aata hai
- @Transactional(rollbackFor = Exception.class) mein specified exception aati hai

### 8. Transaction ke saath exception handling kaise karein?

Exception handling ke liye:

```java
@Transactional(rollbackFor = {SQLException.class, DataAccessException.class})
public void someMethod() {
    try {
        // database operations
    } catch (Exception e) {
        // handle exception
    }
}
```

### 9. Nested transactions kaise kaam karte hain?

Nested transactions ke liye @Transactional(propagation = Propagation.NESTED) use karte hain. Agar outer transaction rollback hota hai to nested transaction bhi rollback ho jata hai.

### 10. Transaction ke saath readOnly property ka kya use hai?

readOnly = true set karne se performance improve hoti hai kyunki:

- Hibernate dirty checking nahi karta
- Database locks nahi lagte
- Optimizations apply hote hain

### 11. Multiple databases ke saath transaction kaise handle karein?

Multiple databases ke liye:

- XA transactions use karein
- JTA (Java Transaction API) use karein
- @Transactional(transactionManager = "specificTransactionManager") use karein

### 12. Transaction ke saath pagination kaise karein?

Pagination ke liye:

```java
@Transactional(readOnly = true)
public Page<Entity> getPaginatedData(Pageable pageable) {
    return repository.findAll(pageable);
}
```

### 13. Transaction ke saath batch operations kaise karein?

Batch operations ke liye:

```java
@Transactional
public void batchInsert(List<Entity> entities) {
    for (Entity entity : entities) {
        repository.save(entity);
    }
}
```

### 14. Transaction ke saath optimistic locking kaise implement karein?

Optimistic locking ke liye:

```java
@Entity
public class Entity {
    @Version
    private Long version;
    // other fields
}
```

### 15. Transaction ke saath pessimistic locking kaise implement karein?

Pessimistic locking ke liye:

```java
@Lock(LockModeType.PESSIMISTIC_WRITE)
@Query("select e from Entity e where e.id = :id")
Entity findByIdForUpdate(@Param("id") Long id);
```

### 16. Transaction ke saath auditing kaise implement karein?

Auditing ke liye:

```java
@EntityListeners(AuditingEntityListener.class)
@Entity
public class Entity {
    @CreatedDate
    private LocalDateTime createdDate;
    @LastModifiedDate
    private LocalDateTime lastModifiedDate;
}
```

### 17. Transaction ke saath caching kaise implement karein?

Caching ke liye:

```java
@Cacheable("entities")
@Transactional(readOnly = true)
public Entity findById(Long id) {
    return repository.findById(id).orElse(null);
}
```

### 18. Transaction ke saath retry mechanism kaise implement karein?

Retry mechanism ke liye:

```java
@Retryable(maxAttempts = 3, backoff = @Backoff(delay = 1000))
@Transactional
public void someMethod() {
    // method code
}
```

### 19. Transaction ke saath validation kaise implement karein?

Validation ke liye:

```java
@Validated
@Transactional
public void saveEntity(@Valid Entity entity) {
    repository.save(entity);
}
```

### 20. Transaction ke saath performance optimization kaise karein?

Performance optimization ke liye:

- readOnly = true use karein where possible
- Batch operations use karein
- Proper indexing karein
- Lazy loading use karein
- Caching implement karein
- Connection pooling use karein

## 📘 Transactionality – Spring Data JPA

### 🔹 1. CrudRepository ke methods ka by default transaction behaviour

Spring Data JPA me jo methods `CrudRepository` se inherit hote hai (jaise `findAll()`, `save()`, `delete()`), unpe already `@Transactional` annotation apply hota hai.

- **Read methods** (jaise `findAll`, `findById`) ke upar:  
  ➤ `@Transactional(readOnly = true)` laga hota hai.  
  ➤ Matlab: Ye method sirf data padhega, kuch change nahi karega.

- **Write methods** (jaise `save`, `delete`):  
  ➤ `@Transactional` hota hai without `readOnly = true`.  
  ➤ Matlab: Ye data ko update ya delete bhi kar sakta hai.

### 🔹 2. Agar kisi method ka transaction alag rakhna ho toh?

Agar tumhe kisi specific method ka transaction alag tarike se set karna hai (jaise timeout, readOnly false karna), toh tum us method ko **redeclare** kar sakte ho apne interface me.

#### ✅ Example:

```java
public interface UserRepository extends CrudRepository<User, Long> {

  @Override
  @Transactional(timeout = 10)
  public List<User> findAll();
}
```

📌 Iska matlab:

- `findAll()` method ab 10 second me complete hona chahiye.
- Ab ye method `readOnly` bhi nahi hai, matlab data change bhi kar sakta hai.

### 🔹 3. Service ya Facade use karke transactions define karna (Best Practice)

Zyada tar production code me **repository me transaction lagane ke bajaye**, ek **Service class** banti hai jisme `@Transactional` use hota hai. Ye class ek ya zyada repositories ke methods ko call karti hai.

#### ✅ Example:

```java
@Service
public class UserManagementImpl implements UserManagement {

  private final UserRepository userRepository;
  private final RoleRepository roleRepository;

  public UserManagementImpl(UserRepository userRepository, RoleRepository roleRepository) {
    this.userRepository = userRepository;
    this.roleRepository = roleRepository;
  }

  @Transactional
  public void addRoleToAllUsers(String roleName) {
    Role role = roleRepository.findByName(roleName);

    for (User user : userRepository.findAll()) {
      user.addRole(role);
      userRepository.save(user);
    }
  }
}
```

📌 Samjho:

- Ye pura `addRoleToAllUsers()` method ek hi transaction ke andar chalega.
- Agar beech me kuch fail ho gaya toh sab rollback ho jayega.
- `userRepository` aur `roleRepository` dono ke andar ke transaction config ignore ho jayenge.
- Sirf service wale method ka `@Transactional` chalega.

📌 Note: `@EnableTransactionManagement` jaroor hona chahiye config me.

### 🔹 4. Query methods me @Transactional ka use

Spring Data JPA me query methods (jaise `findByLastname`) pe by default koi transaction config nahi hota. Agar tumhe `readOnly` ya `write` config chahiye toh tum `@Transactional` manually laga sakte ho.

#### ✅ Example:

```java
@Transactional(readOnly = true)
interface UserRepository extends JpaRepository<User, Long> {

  List<User> findByLastname(String lastname);

  @Modifying
  @Transactional
  @Query("delete from User u where u.active = false")
  void deleteInactiveUsers();
}
```

📌 Samjho:

- `findByLastname()` sirf data read karega → `readOnly=true` lagaya.
- `deleteInactiveUsers()` ek delete query hai → `@Modifying` + `@Transactional` lagana zaroori hai.

### 🔹 5. readOnly=true ka real kaam kya hai?

- Ye **performance optimization** ke liye hota hai.
- JDBC driver aur Hibernate ko batata hai ki ye query sirf read kar rahi hai, kuch write nahi.
- Agar Hibernate use ho raha hai, toh `flush mode = NEVER` ho jata hai, jisse dirty checking nahi hoti → performance fast.

### ✅ Final Advice:

- Read ke liye: `@Transactional(readOnly = true)`
- Write ke liye: `@Transactional`
- Service level par `@Transactional` use karna best practice hai.

### 📑 10 Important Questions (Practice ke liye):

1. Spring Data JPA me `findAll()` method by default kis transaction config ke sath chalta hai?
2. `@Transactional(readOnly = true)` ka kya use hai?
3. Agar kisi method me timeout set karna ho toh kaise karenge?
4. Service layer me `@Transactional` lagane ka kya fayda hai?
5. `@Modifying` annotation kab lagta hai?
6. Repository ke andar ke `@Transactional` ko kab ignore kiya jata hai?
7. Hibernate me `flush mode = NEVER` ka kya matlab hota hai?
8. Facade pattern me transaction kaise handle hota hai?
9. `readOnly=true` hone ke bawajood kya query update kar sakti hai?
10. `@Transactional` aur `@Transactional(readOnly = true)` me kya difference hai?

## 🔐 Locking – Spring Data JPA

### 🔸 Locking kya hota hai?

Agar 2 users ek hi data pe same time pe kaam kare (jaise ek read kar raha, aur doosra write), toh data corrupt ho sakta hai. Isliye hum **locking** use karte hai – taaki jab tak ek banda ka kaam pura na ho, koi dusra interfere na kare.

### 🔸 Lock lagane ka tariqa Spring Data JPA me

Agar kisi method pe lock lagana hai, toh simple `@Lock` annotation use karo. Ye annotation batata hai ki method kis type ka lock use karega – read ya write.

### ✅ Example 1: Query method pe lock lagana

```java
interface UserRepository extends Repository<User, Long> {

  @Lock(LockModeType.READ)
  List<User> findByLastname(String lastname);
}
```

🧠 iska matlab:  
Jab `findByLastname()` chalega, toh us query pe **READ lock** lagega.  
Koi aur banda usi time pe wo data **update** nahi kar payega. Sirf read chalega safely.

### ✅ Example 2: CRUD method pe bhi lock lag sakta hai

```java
interface UserRepository extends Repository<User, Long> {

  @Lock(LockModeType.READ)
  List<User> findAll();
}
```

🧠 iska matlab:  
`findAll()` ab READ lock ke sath chalega.  
Koi aur us data ko modify nahi kar sakta jab tak current user ka kaam complete na ho jaye.

### 🔸 Common LockModeType values

| Lock type                        | Kaam kya karta hai                        |
| -------------------------------- | ----------------------------------------- |
| `READ`                           | doosra banda update nahi kar sakta        |
| `WRITE` (ya `PESSIMISTIC_WRITE`) | koi bhi read ya write nahi kar sakta      |
| `OPTIMISTIC`                     | version check karta hai – advance locking |

### 🔸 Kab use karna chahiye?

- Jab **same record pe multiple threads** ya users ka access ho raha ho.
- Jab **data integrity** kaafi important ho.
- Jab **race condition** ya update clash avoid karna ho.

### 📑 10 Questions (Practice ke liye):

1. Locking ka main purpose kya hota hai?
2. `@Lock(LockModeType.READ)` ka matlab kya hai?
3. CRUD method pe lock lagana ho toh kya karna padta hai?
4. `WRITE` lock aur `READ` lock me kya farak hai?
5. Agar 2 threads ek saath same row ko access kare, toh `@Lock` kaise help karega?
6. `OPTIMISTIC` locking kis use-case me sahi hoti hai?
7. Lock lagane se performance pe kya impact padta hai?
8. Kya `@Lock` sirf query methods ke liye hai?
9. JPA me locking kis level pe apply hota hai – method ya entity?
10. Kya `findAll()` method pe bhi lock lagaya ja sakta hai?

## 🧩 Merging Persistence Units – Spring Data JPA

### 🔸 Problem kya hota hai?

Maan le tu ek **modular application** bana raha hai — matlab alag-alag modules hai like: `user`, `order`, `billing` — aur sabka apna alag persistence unit hai.

But tu chah raha hai ki saare modules **ek hi persistence unit ke andar** kaam kare — taaki data consistency bani rahe aur multiple entity managers na banane padey.

### 🔸 Spring iska solution kya deta hai?

Spring bolta hai ki tu **MergingPersistenceUnitManager** use kar. Ye manager alag-alag persistence units ko **unke name ke basis pe merge** kar deta hai ek hi unit me.

### ✅ Example 1: MergingPersistenceUnitManager ka use

```xml
<bean class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
  <property name="persistenceUnitManager">
    <bean class="org.springframework.data.jpa.support.MergingPersistenceUnitManager" />
  </property>
</bean>
```

🧠 iska matlab:

- Tera app agar multiple modules se persistence units le raha hai, toh ye manager **un sabko merge** karke ek hi `EntityManagerFactory` banata hai.
- Tu easily alag-alag domain modules bana sakta hai, but data management centralized hoga.

## 🔍 Classpath Scanning for @Entity Classes and Mapping Files

### 🔸 Normal JPA me dikkat kya hai?

Normal JPA config (without Spring) me tujhe **har ek @Entity class ko manually orm.xml me likhna padta hai**.

Same goes for XML mapping files — tujhe manually define karna padta hai ki kaunsa mapping file use hoga.

### 🔸 Spring isme help kaise karta hai?

Spring me tu ek **ClasspathScanningPersistenceUnitPostProcessor** use kar sakta hai, jo automatically scan karega:

- `@Entity` classes
- `@MappedSuperclass` classes
- Mapping files (jaise `UserMapping.xml`, `OrderMapping.xml`)

### ✅ Example 2: Entity classes scan karne ka setup

```xml
<bean class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
  <property name="persistenceUnitPostProcessors">
    <list>
      <bean class="org.springframework.data.jpa.support.ClasspathScanningPersistenceUnitPostProcessor">
        <constructor-arg value="com.acme.domain" />
        <property name="mappingFileNamePattern" value="**/*Mapping.xml" />
      </bean>
    </list>
  </property>
</bean>
```

🧠 iska matlab:

- Ye processor `com.acme.domain` package me jaake sari `@Entity` classes dhoond lega.
- Saath me jo files `*Mapping.xml` pattern pe match ho rahi hongi, unko bhi automatically config me daal dega.

### 🔸 Spring 3.1 se aur easy ho gaya

Ab tu directly `LocalContainerEntityManagerFactoryBean` ke andar hi **package to scan** de sakta hai:

```xml
<property name="packagesToScan" value="com.acme.domain" />
```

📌 iska fayda: Tu XML mapping se bach jaata hai, aur sab kuch automatically scan ho jaata hai.

### 📑 10 Questions (Practice ke liye):

1. MergingPersistenceUnitManager ka kaam kya hai?
2. Agar app me multiple modules ho toh persistence units kaise handle karenge?
3. `@Entity` class ko auto-detect karne ke liye Spring kya deta hai?
4. `ClasspathScanningPersistenceUnitPostProcessor` kya karta hai?
5. `mappingFileNamePattern` ka kya role hai config me?
6. Entity classes scan karne ke liye kis property ka use hota hai Spring 3.1 ke baad?
7. Default JPA setup me `@Entity` classes kaise register karte hai?
8. `persistenceUnitPostProcessors` kiske under likhte hai?
9. Agar tu `billing` aur `orders` dono module me same persistence unit use karna chahe toh kya karega?
10. `LocalContainerEntityManagerFactoryBean` kis kaam aata hai?

## 🧩 Custom Repository Implementation – Spring Data JPA

### 🔸 Problem kya hota hai?

Spring Data me tu mostly query methods bana sakta hai like `findByEmail()`, `findByName()` etc — bina kuch coding ke.  
**But** agar tujhe koi custom logic chahiye (like: JDBC call, native query, complex business rule)  
→ tab tu **custom method** likh sakta hai apne repository me.

## 🔧 Customization ka process – step by step

### ✅ Step 1: Pehle ek **custom interface** bana

```java
interface CustomizedUserRepository {
  void someCustomMethod(User user);
}
```

### ✅ Step 2: Us interface ka **Impl class** bana

```java
class CustomizedUserRepositoryImpl implements CustomizedUserRepository {

  @Override
  public void someCustomMethod(User user) {
    // Custom code likh yahan
  }
}
```

🧠 NOTE: `Impl` suffix mandatory hai — Spring isi se samajhta hai ki ye us interface ka implementation hai.

### ✅ Step 3: Apne main repository me us interface ko extend karo

```java
interface UserRepository extends CrudRepository<User, Long>, CustomizedUserRepository {
  // normal query methods bhi likh sakta hai
}
```

📌 Ab jab tu `UserRepository` ko inject karega, tujhe `someCustomMethod()` bhi milega.

## 🔸 Fragment Model (Recommended)

Aajkal Spring recommend karta hai **fragment-based model**:

- Tera repository multiple custom interfaces extend kare
- Har interface ka alag `Impl` ho
- Ye sab milke ek **composed repository** banate hai

### ✅ Example: Multiple fragments

```java
interface HumanRepository {
  void someHumanMethod(User user);
}
class HumanRepositoryImpl implements HumanRepository {
  public void someHumanMethod(User user) { … }
}

interface ContactRepository {
  void someContactMethod(User user);
}
class ContactRepositoryImpl implements ContactRepository {
  public void someContactMethod(User user) { … }
}
```

```java
interface UserRepository extends CrudRepository<User, Long>, HumanRepository, ContactRepository {
  // sab methods available ho jaenge
}
```

## 💾 Custom `save()` override karna

```java
interface CustomizedSave<T> {
  <S extends T> S save(S entity);
}
class CustomizedSaveImpl<T> implements CustomizedSave<T> {
  public <S extends T> S save(S entity) {
    // custom save logic
  }
}
```

```java
interface UserRepository extends CrudRepository<User, Long>, CustomizedSave<User> {}
```

## 🧠 Configuration Options

### ✅ 1. Custom Impl postfix change karna:

```java
@EnableJpaRepositories(repositoryImplementationPostfix = "MyPostfix")
```

- Ab Spring `CustomizedUserRepositoryMyPostfix` dhundhega instead of default `Impl`.

### ✅ 2. Agar dono packages me same naam ka Impl ho toh?

Spring match karta hai:

- **Bean name + Impl suffix** → jo match karega wahi lega.
- Tu `@Component("specialCustomImpl")` laga ke priority set kar sakta hai.

### ✅ 3. Agar tu manual wiring kare (special beans inject karne ke liye):

```java
class MyClass {
  MyClass(@Qualifier("userRepositoryImpl") UserRepository userRepository) {
    …
  }
}
```

## 🔍 Fragment external location me ho toh?

Spring bas repository ke package ke under ka scan karta hai.

Agar tu external library ya dusri location se fragment la raha ho toh usko `spring.factories` me register karna padega:

```
# META-INF/spring.factories
com.acme.search.SearchExtension = com.acme.search.DefaultSearchExtension
```

## 📖 Real-life Use Case – Search Extension

```java
interface SearchExtension<T> {
  List<T> search(String text, Limit limit);
}
class DefaultSearchExtension<T> implements SearchExtension<T>, RepositoryMetadataAccess {
  public List<T> search(String text, Limit limit) {
    // search index call via SearchService
  }
}
```

→ Tu isko register karega spring.factories me  
→ Fir kisi bhi repo me `extends SearchExtension<T>` likh ke use kar sakta hai

## ⚙️ Customize Base Repository for ALL

```java
class MyRepositoryImpl<T, ID> extends SimpleJpaRepository<T, ID> {
  private final EntityManager em;
  public MyRepositoryImpl(JpaEntityInformation info, EntityManager em) {
    super(info, em);
    this.em = em;
  }

  @Override
  @Transactional
  public <S extends T> S save(S entity) {
    // custom save
  }
}
```

```java
@EnableJpaRepositories(repositoryBaseClass = MyRepositoryImpl.class)
```

## 📌 Bonus: Multiple EMs ho toh `JpaContext` use karo

```java
class UserRepositoryImpl implements UserRepositoryCustom {
  private final EntityManager em;

  @Autowired
  public UserRepositoryImpl(JpaContext context) {
    this.em = context.getEntityManagerByManagedType(User.class);
  }
}
```

📌 Fayda: Tu easily correct EM assign kar sakta hai — agar multiple persistence units ho toh bhi koi dikkat nahi.

## 📑 10 Practice Questions (Tere Style Me)

1. Custom repository method banane ke liye pehle kya define karna padta hai?
2. Impl class ka naam kaise hona chahiye?
3. Agar tu `save()` ko override karna chahe toh kya karega?
4. Fragment-based repository ka kya fayda hai?
5. Agar tu multiple custom interfaces use kare ek repository me toh kaise karega?
6. `spring.factories` me custom fragment kaise register hota hai?
7. Base class ko customize karne ka proper tarika kya hai?
8. `JpaContext` kis problem ko solve karta hai?
9. Custom implementation me manually bean inject karna ho toh kaise karega?
10. `repositoryImplementationPostfix` ka kya use hai?

## 📢 Publishing Events from Aggregate Roots – Spring Data

### 🔸 Basic Concept

Spring Data ke according, jab tu kisi `Entity` ko repository se save ya delete karta hai,  
aur wo entity agar ek **aggregate root** hai (matlab top-level domain object),  
toh tu uske through **domain events** publish kar sakta hai.

### 🔸 Kyu karte hai domain event publish?

- DDD (Domain Driven Design) me jab koi **important kaam** complete hota hai (jaise `OrderPlaced`, `UserRegistered`), toh hum uska **event** publish karte hai.
- Isse system loosely coupled rehta hai aur alag module react kar sakte hai bina tightly connected huye.

## ✅ Spring Data me kaise publish kare event?

### Step 1️⃣: Entity ke andar ek method bana jisme `@DomainEvents` laga ho

```java
class AnAggregateRoot {

  @DomainEvents
  Collection<Object> domainEvents() {
      // Yahan se events return honge
      return List.of(new SomethingHappenedEvent(this));
  }
}
```

🧠 Iska matlab:

- Jab tu is object ko save karega (ya delete), to `domainEvents()` method chalega.
- Jo bhi event return karega, Spring usko publish karega.

### Step 2️⃣: Clean-up method (optional but useful)

```java
  @AfterDomainEventPublication
  void callbackMethod() {
     // event list ko clear karna ho toh yahan kare
  }
}
```

🧠 Iska matlab:

- Jaise hi saare events publish ho jaye, ye method call hoga.
- Tu yahan list clean kar sakta hai ya log likh sakta hai ya kuch aur.

## 🔁 Ye methods kab chalega?

Jab tu Spring Data repository ke ye methods call kare:

| Method               | Event Triggered?                                        |
| -------------------- | ------------------------------------------------------- |
| `save()`             | ✅ YES                                                  |
| `saveAll()`          | ✅ YES                                                  |
| `delete()`           | ✅ YES                                                  |
| `deleteAll()`        | ✅ YES                                                  |
| `deleteAllInBatch()` | ✅ YES                                                  |
| `deleteInBatch()`    | ✅ YES                                                  |
| `deleteById()`       | ❌ NO (kyunki wo aggregate instance load hi nahi karta) |

🧠 `deleteById()` se event publish nahi hoga, kyunki usme object ki instance hoti hi nahi.

## 📑 Practice Questions (tere style me):

1. `@DomainEvents` kis method pe lagate hai?
2. `domainEvents()` method kya return karta hai?
3. `@AfterDomainEventPublication` ka use kya hai?
4. `deleteById()` se event publish kyu nahi hota?
5. Kaunse repository methods se domain events publish hote hai?
6. Agar tu `List<Object>` ke bajaye single event return kare to chalega?
7. `@DomainEvents` method me arguments hone chahiye kya?
8. Agar event publish hone ke baad kuch clean karna ho toh kaunsa method use karega?
9. Event system use karne ka fayda kya hai DDD ke perspective se?
10. Kya ye event Spring ApplicationEvent ke sath integrate ho sakta hai?

## ❓ Null Handling in Spring Data JPA

### 🔸 Basic Idea:

Spring Data 2.0 se CRUD aur query methods me **null handle karne ka system clean aur safe ho gaya hai**.  
Ab tu **Optional**, **@Nullable**, aur **null-safe defaults** use kar sakta hai for better control and safer code.

### ✅ Query Method Return Types – kya kya return ho sakta hai?

| Return Type             | Jab result nahi milta to?            |
| ----------------------- | ------------------------------------ |
| `Optional<T>`           | returns `Optional.empty()`           |
| `@Nullable T`           | returns `null`                       |
| `T` (non-nullable)      | throws exception if result not found |
| `List<T>`               | returns empty list `[]`              |
| `Stream<T>`             | returns empty stream                 |
| `Set<T>` or other coll. | returns empty collection             |

### ✅ Popular supported wrappers:

- `java.util.Optional` → ✅ recommended
- `com.google.common.base.Optional`
- `scala.Option`
- `io.vavr.control.Option`

📌 But agar tu wrapper use nahi karta, to Spring null ya exception return karega based on annotations.

## ⚠️ Important Annotations for Null Handling

### 🔹 `@NonNullApi` → **Package level pe lagta hai**

```java
@org.springframework.lang.NonNullApi
package com.acme;
```

🧠 iska matlab:

- Package ke andar jitne bhi method return type/parameters hai — unka **default non-null** maana jaayega.
- Agar koi method `null` return karega, to **runtime exception** throw hoga.

### 🔹 `@NonNull` → individual param ya method pe laga sakta hai

(But mostly zarurat nahi padti agar tu `@NonNullApi` already laga chuka hai)

### 🔹 `@Nullable` → jab explicitly tu batana chahe ki null allowed hai

```java
@Nullable
User findByEmailAddress(@Nullable EmailAddress email);
```

🧠 iska matlab:

- null query param allowed hai
- agar result nahi mila to `null` return hoga — no exception

## ✅ Practical Example – Full Setup

```java
package com.acme;

import org.springframework.lang.Nullable;

interface UserRepository extends Repository<User, Long> {

  User getByEmailAddress(EmailAddress emailAddress);

  @Nullable
  User findByEmailAddress(@Nullable EmailAddress emailAddress);

  Optional<User> findOptionalByEmailAddress(EmailAddress emailAddress);
}
```

### 🔍 Breakdown:

1. **getByEmailAddress(...)**  
   → Non-null by default  
   → `null` return hua to exception  
   → `null` param diya to `IllegalArgumentException`

2. **findByEmailAddress(...) with @Nullable**  
   → `null` param allowed  
   → `null` return bhi allowed

3. **findOptionalByEmailAddress(...)**  
   → param `null` ho toh exception  
   → result na mile to `Optional.empty()` return

## 🤖 Kotlin Support

Kotlin me nullability language ka part hota hai. Tu aise likhta hai:

```kotlin
interface UserRepository : Repository<User, String> {
  fun findByUsername(username: String): User        // non-null param, non-null result
  fun findByFirstname(firstname: String?): User?    // param aur result dono nullable
}
```

🧠 Kotlin automatically compiler-level check karta hai:

- null pass karna ya return karna allowed hai ya nahi

📦 Make sure `kotlin-reflect` jar laga ho — warna runtime pe null metadata kaam nahi karega.

## 📑 Practice Questions (tere style me):

1. Agar tu `Optional<User>` return karega to result na mile to kya milega?
2. `@NonNullApi` ka kya use hai?
3. `@Nullable` kis case me use karte hai?
4. Agar tu `T` return kare bina wrapper ke, to result null ho to kya hoga?
5. `deleteById()` me null return ka chance hai kya?
6. Tu Kotlin me `User?` likhta hai to iska matlab kya hota hai?
7. Spring Data me `List<T>` agar result na mile to kya return karega?
8. `@Nullable` parameter aur return me dono use karne se kya fayda hai?
9. Spring Data me null-safe coding ke liye best practices kya hai?
10. Tu `Optional<T>` kab prefer karega `@Nullable` ke jagah?

## 📘 Spring Data Web Support — Book Style Notes

## 🔹 1. PagedModel Output (Pagination with metadata)

### Controller Code:

```java
@GetMapping("/page")
PagedModel<?> page(Pageable pageable) {
  return new PagedModel<>(repository.findAll(pageable));
}
```

### JSON Output:

```json
{
  "content": [ … ],      // data list
  "page": {
    "size": 20,
    "totalElements": 30,
    "totalPages": 2,
    "number": 0
  }
}
```

🧠 Page ka metadata bhi JSON me aata hai → size, total pages, page number.

### ✅ Globally simplified rendering enable karna:

```java
@EnableSpringDataWebSupport(pageSerializationMode = VIA_DTO)
class MyConfiguration { }
```

🧠 Isse tu controller me `Page` hi return karega, but output JSON me **PagedModel jaisa** milega.

```java
@GetMapping("/page")
Page<?> page(Pageable pageable) {
  return repository.findAll(pageable);
}
```

## 🔹 2. Hypermedia Support (HAL, links, navigation)

### Controller with Assembler:

```java
@GetMapping("/people")
HttpEntity<PagedModel<Person>> people(Pageable pageable,
  PagedResourcesAssembler<Person> assembler) {

  Page<Person> people = repository.findAll(pageable);
  return ResponseEntity.ok(assembler.toModel(people));
}
```

### JSON Output with links:

```json
{
  "links": [
    { "rel": "next", "href": "http://localhost:8080/people?page=1&size=20" }
  ],
  "content": [ … ],
  "page": {
    "size": 20,
    "totalElements": 30,
    "totalPages": 2,
    "number": 0
  }
}
```

🧠 `PagedResourcesAssembler.toModel()`:

- page → metadata deta hai
- links → prev, next, self generate karta hai
- content → Page ka actual data

🔔 Hypermedia enable karne ke liye:

```java
@EnableHypermediaSupport(type = HypermediaType.HAL)
```

## 🔹 3. Spring Data Jackson Modules (geo types, etc.)

Agar tu geo types use kare (like Point, Circle), to ye classes:

- `org.springframework.data.geo.Distance`
- `org.springframework.data.geo.Point`
- `Circle`, `Box`, `Polygon`

🧠 Automatically Jackson ke ObjectMapper me register ho jaate hai agar:

- Web support enable hai
- Jackson ObjectMapper available hai

## 🔹 4. Web Data Binding using JSONPath / XPath (Projections)

### Projection Interface:

```java
@ProjectedPayload
public interface UserPayload {
  @XBRead("//firstname")
  @JsonPath("$..firstname")
  String getFirstname();

  @XBRead("/lastname")
  @JsonPath({ "$.lastname", "$.user.lastname" })
  String getLastname();
}
```

🧠 Isse tu request payload se **dynamically firstname/lastname extract** kar sakta hai.

Use cases:

## 📘 Spring Data JPA – Query Method Keywords

## 🔹 1. Subject Keywords – Method kis type ka kaam karega?

Ye batate hain ki tumhara method **kya kaam karega** – find, count, delete, exists, etc.

| Keyword      | Kaam kya karta hai                | Example                        |
| ------------ | --------------------------------- | ------------------------------ |
| `find…By`    | Entity ya list return karta hai   | `findByName()`                 |
| `read…By`    | Same as find                      | `readByEmail()`                |
| `get…By`     | Same as find                      | `getByUsername()`              |
| `query…By`   | Same as find                      | `queryByCity()`                |
| `search…By`  | Same as find                      | `searchByPhone()`              |
| `stream…By`  | Stream return karega              | `streamByType()`               |
| `exists…By`  | `boolean` return karega           | `existsByEmail()`              |
| `count…By`   | `long` ya `int` return karega     | `countByStatus()`              |
| `delete…By`  | Delete karega, void/int return    | `deleteById()`                 |
| `remove…By`  | Same as delete                    | `removeByToken()`              |
| `…First<N>…` | N results limit karega            | `findFirst3ByOrderByNameAsc()` |
| `…Top<N>…`   | Same as First                     | `findTop5ByAgeGreaterThan(25)` |
| `…Distinct…` | Duplicate results hata ke laayega | `findDistinctByCity()`         |

## 🔹 2. Reserved Methods (CrudRepository ke predefined methods)

| Method Name          | Kaam kya karta hai           |
| -------------------- | ---------------------------- |
| `deleteById(id)`     | Ek record delete             |
| `deleteAllById(ids)` | Multiple record delete       |
| `existsById(id)`     | boolean check karta hai      |
| `findAllById(ids)`   | List of matched IDs          |
| `findById(id)`       | Optional<T> return karta hai |

## 🔹 3. Predicate Keywords – WHERE clause banate hain

Ye keywords tumhare method ke name me likhe jaate hain jo query ka condition set karte hain.

### ✅ Logical Conditions

| Keyword | Example                 |
| ------- | ----------------------- |
| `And`   | `findByCityAndStatus()` |
| `Or`    | `findByAgeOrCity()`     |

### ✅ Date Conditions

| Keyword               | Example                        |
| --------------------- | ------------------------------ |
| `After` / `IsAfter`   | `findByCreatedDateAfter(...)`  |
| `Before` / `IsBefore` | `findByCreatedDateBefore(...)` |

### ✅ String Conditions

| Keyword                  | Kaam        | Example                          |
| ------------------------ | ----------- | -------------------------------- |
| `Containing`, `Contains` | LIKE %...%  | `findByNameContaining("vi")`     |
| `StartingWith`           | LIKE "...%" | `findByNameStartingWith("Ra")`   |
| `EndingWith`             | LIKE "%..." | `findByNameEndingWith("sh")`     |
| `Like`                   | Custom LIKE | `findByEmailLike("%@gmail.com")` |

### ✅ Comparison Operators

| Keyword            | Meaning | Example                             |
| ------------------ | ------- | ----------------------------------- |
| `GreaterThan`      | >       | `findByAgeGreaterThan(18)`          |
| `GreaterThanEqual` | >=      | `findByAgeGreaterThanEqual(18)`     |
| `LessThan`         | <       | `findBySalaryLessThan(50000)`       |
| `LessThanEqual`    | <=      | `findBySalaryLessThanEqual(100000)` |

### ✅ Null / Empty Checks

| Keyword                  | Example                   |
| ------------------------ | ------------------------- |
| `IsNull`, `Null`         | `findByEmailIsNull()`     |
| `IsNotNull`, `NotNull`   | `findByMobileIsNotNull()` |
| `IsEmpty`, `Empty`       | `findByRolesIsEmpty()`    |
| `IsNotEmpty`, `NotEmpty` | `findByRolesIsNotEmpty()` |

### ✅ Boolean Checks

| Keyword            | Example                 |
| ------------------ | ----------------------- |
| `True`, `IsTrue`   | `findByActiveIsTrue()`  |
| `False`, `IsFalse` | `findByActiveIsFalse()` |

### ✅ Collection & Range

| Keyword                | Example                      |
| ---------------------- | ---------------------------- |
| `In`, `IsIn`           | `findByCityIn(List<String>)` |
| `NotIn`, `IsNotIn`     | `findByCityNotIn(...)`       |
| `Between`, `IsBetween` | `findByAgeBetween(20, 30)`   |

### ✅ Geospatial (if supported)

| Keyword              | Description                      |
| -------------------- | -------------------------------- |
| `Near`, `IsNear`     | Find by coordinates near a point |
| `Within`, `IsWithin` | Check inside a geo shape         |

## 🔹 4. Modifier Keywords

Modifiers jo comparison ke behavior ko modify karte hain.

| Modifier                     | Kaam kya karta hai                 | Example                                        |
| ---------------------------- | ---------------------------------- | ---------------------------------------------- |
| `IgnoreCase`, `IgnoringCase` | Case-insensitive match             | `findByEmailIgnoreCase(...)`                   |
| `AllIgnoreCase`              | Sabhi string fields me ignore case | `findByFirstNameAndLastNameAllIgnoreCase(...)` |
| `OrderBy<Field>Asc/Desc`     | Sorting ke liye                    | `findByCityOrderByNameAsc()`                   |

## ✅ Examples – Full method names

```java
List<User> findTop3ByAgeGreaterThanOrderByNameAsc(int age);

Optional<User> findByUsernameIgnoreCase(String username);

boolean existsByEmail(String email);

long countByStatus(String status);

void deleteByCity(String city);
```

## 📑 Practice Questions (Tere Style Me)

1. `findFirst5ByOrderByAgeDesc()` ka kya karega?
2. `findByUsernameContainingIgnoreCase()` ka meaning kya hai?
3. `existsByMobile()` kis type ka result dega?
4. `countByRole()` kis return type ka method hota hai?
5. `findByDobBetween()` me kya pass karte hai?
6. `findByEmailIsNull()` aur `IsNotNull()` ka use kab karte hai?
7. `OrderBy…Asc/Desc` kis part me likhte hai method name ke?
8. Agar method `findByCityIn(...)` likha ho to parameter me kya dena padega?
9. `deleteByStatus()` method kya return karega?
10. `findTop3ByNameStartsWith("Ra")` kis type ka result dega?

## 📘 Repository Query Return Types – Spring Data JPA

## 🔹 Basic Idea:

Spring Data me tu jab query method likhta hai (`findByXyz()`), to uska **return type important hota hai**.

Spring automatically decide karta hai:

- **Single result milega ya list**
- **Optional hona chahiye ya nahi**
- **Stream ya Page chahiye**
- **Reactive result chahiye ya synchronous**

## ✅ Table: Common Return Types – Explanation ke sath

| Return Type                | Kya karta hai                            | Special Notes                     |
| -------------------------- | ---------------------------------------- | --------------------------------- |
| `void`                     | Return nahi karta kuch                   | mostly delete/update              |
| `T`                        | 1 entity return karega                   | Agar 1 se zyada mila → exception  |
| `Optional<T>`              | 0 ya 1 result                            | Best for null-safe check          |
| `List<T>`, `Collection<T>` | List of results                          | Never null, empty list if nothing |
| `Iterator<T>`              | Java Iterator                            | rarely used                       |
| `Stream<T>`                | Lazy stream of data                      | Close karna padta hai manually    |
| `Streamable<T>`            | Advanced iterable                        | Map, filter support karta hai     |
| `Page<T>`                  | List with metadata (page, total etc.)    | `Pageable` parameter mandatory    |
| `Slice<T>`                 | List with info: "next page hai ya nahi?" | Lightweight than Page             |
| `Window<T>`                | For scrollable results                   | Needs ScrollPosition param        |
| `Future<T>`                | Async result (Spring @Async)             | Synchronous call nahi chalega     |
| `CompletableFuture<T>`     | Java 8 async                             | Needs `@Async`                    |
| `Mono<T>`                  | 0 or 1 result (Reactive)                 | Reactor Project                   |
| `Flux<T>`                  | 0 or many result (Reactive)              | Stream of data                    |
| `Single<T>`                | RxJava: exactly 1 result                 | Error if empty/multiple           |
| `Maybe<T>`                 | RxJava: 0 or 1                           | Like Optional                     |
| `Flowable<T>`              | RxJava: stream of data                   | Like Flux                         |
| `GeoResult<T>`             | Result with distance info                | Geospatial only                   |
| `GeoResults<T>`            | List of GeoResult<T>                     | Only if store supports geo        |
| `GeoPage<T>`               | Page + geo info                          | Geo + Paging                      |

## 🔹 Examples:

```java
Optional<User> findByEmail(String email);
// return Optional.empty() if not found

List<User> findByAgeGreaterThan(int age);
// return empty list if none

Page<User> findByCity(String city, Pageable pageable);
// return paged result with metadata

Stream<Product> streamByType(String type);
// stream result (lazy), needs to be closed

Mono<User> findById(String id);
// for reactive MongoDB or R2DBC
```

## ⚠️ Important Notes:

1. **T** or `Optional<T>` → agar 1 se zyada result mila to exception aayega.
2. `List`, `Page`, `Stream`, etc. → kabhi `null` nahi dete. Agar kuch nahi mila to empty list/stream return hota hai.
3. **Reactive return types** (`Mono`, `Flux`) → tabhi use karo jab tu reactive repository use kar raha ho.
4. `Pageable` aur `ScrollPosition` jaisa parameter compulsory hai jab tu `Page<T>` ya `Window<T>` return type use karta hai.

## 📑 Practice Questions (tere style me):

1. `Optional<User> findByEmail(...)` me agar user na mile to kya hoga?

## 📘 Spring Data JPA – FAQ Notes (Common + Auditing)

### ❓ Q1: Mujhe `JpaRepository` ke methods ka detailed log chahiye, jaise kya call ho raha hai, kya return ho raha hai. Kaise karu?

👉 Answer:  
Use karo **`CustomizableTraceInterceptor`** (Spring AOP based logging).

### ✅ XML Config Example:

```xml
<bean id="customizableTraceInterceptor"
      class="org.springframework.aop.interceptor.CustomizableTraceInterceptor">
  <property name="enterMessage" value="Entering $[methodName]($[arguments])"/>
  <property name="exitMessage" value="Leaving $[methodName](): $[returnValue]"/>
</bean>

<aop:config>
  <aop:advisor advice-ref="customizableTraceInterceptor"
    pointcut="execution(public * org.springframework.data.jpa.repository.JpaRepository+.*(..))"/>
</aop:config>
```

🧠 Iska matlab:

- Jab bhi koi `JpaRepository` ka method chalega (like `save()`, `findById()`), to tu log dekh payega:
  ```
  Entering findById(1)
  Leaving findById(): Optional[User]
  ```

### ❓ Q2: Meri DB already auto set kar rahi hai `created_date`, `modified_date`, to Spring Data auditing se wo override ho ja raha. Usko kaise band karu?

👉 Answer:  
Use karo `<auditing:set-dates="false">` — jo Spring se auto set hone wale dates ko disable karega.

### ✅ XML Config Example:

```xml
<jpa:auditing set-dates="false" />
```

🧠 Iska matlab:

- Tu still `@CreatedDate` aur `@LastModifiedDate` use kar raha hoga,
- But Spring Data un values ko **set nahi karega**, DB khud hi handle karega (e.g., `DEFAULT CURRENT_TIMESTAMP`).

## 📑 Bonus Tips (Tere style me):

- Agar tu logging Spring Boot me karna chahe to `logging.level.org.springframework.data=DEBUG` bhi try kar sakta hai.
- Agar annotation-based auditing disable karna chahe selectively, to `@CreatedDate` ya `@LastModifiedDate` use hi mat kar.

## 💡 Practice Short Qs (revision):

1. `CustomizableTraceInterceptor` kya karta hai?
2. Logging messages me `$[methodName]` ka matlab kya hai?
3. AOP pointcut me `JpaRepository+` ka kya matlab hai?
4. Agar DB khud hi date set kar raha hai, to Spring ko rokne ke liye kya kare?
5. `@CreatedDate` ko use kiya hai but wo overwrite ho raha, solution?
