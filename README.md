# Spring Boot in Hindi

## 📚 Chapter 1: Getting Started with Spring Data JPA

### 1.1 Introduction

Backend application banane mein sabse important cheez hoti hai — data ko store, retrieve aur manage karna.

Agar hum traditional JDBC ka use karein, to kaafi manual coding karni padti hai jaise:

- Database connection banana
- SQL queries likhna
- ResultSet handle karna

Ye process tedious aur error-prone hota hai.

Spring Data JPA humari life easy bana deta hai. Iske through hum kam code likh ke apne database ke saath kaam kar sakte hain.

### 1.2 Apna Project Kaise Setup Kare?

Spring Data JPA project banana bohot aasaan hai. Do tareeke hote hain:

#### 1.2.1 start.spring.io se Project Banana

start.spring.io ek website hai jahan se hum Spring Boot project bana sakte hain.

Bas kuch basic details bharni hoti hain jaise:

- Project type (Maven ya Gradle)
- Java language
- Dependencies: Spring Web, Spring Data JPA, aur Database Driver

Project generate karne ke baad zip file download hoti hai, jisko IDE (jaise IntelliJ, Eclipse) mein import karte hain.

✅ 5 minute mein ek ready project mil jata hai.

#### 1.2.2 Spring Tools Suite (STS) se Project Banana

Agar tum Spring Tools Suite (STS) IDE use karte ho to aur aasaan hai.

New → Spring Starter Project create karo.
Project ka naam aur dependencies select karo.
Aur project tumhare workspace mein aa jata hai ready-made.

✅ STS beginner-friendly IDE hai, specially Spring projects ke liye.

### 1.3 Example Practice Ke Liye

Agar tumko practice karni hai, to Spring Data ke official examples ka ek repository available hota hai.
Usme kaafi real-world based small projects diye hote hain jaise CRUD operation, custom queries waale.

Tum un projects ko download karke khud se run kar sakte ho.
Aur apna concept clear kar sakte ho.

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

**Samjhaav:**

- `@Entity`: Ye class ko database table se map karta hai.
- `@Id`: Id field ko primary key banata hai.
- `@GeneratedValue`: Id automatically generate hogi jab record create hoga.
- `private String name`: Ek normal field hai jisme person ka naam store hoga.

✅ Ab Person class ka har object database mein ek record banega.

#### 1.4.2 Repository Interface (PersonRepository.java)

```java
interface PersonRepository extends Repository<Person, Long> {
  Person save(Person person);
  Optional<Person> findById(long id);
}
```

**Samjhaav:**

- Ye interface Repository ko extend karta hai.
- `save()` method naya Person object database mein save karega.
- `findById()` method id ke basis pe Person object database se laayega.
- Spring khud iska implementation bana dega, hume manually kuch likhne ki zarurat nahi.

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

**Samjhaav:**

- `@SpringBootApplication`: Ye batata hai ki ye Spring Boot application hai.
- `main()`: Application start hoti hai.
- `@Bean CommandLineRunner`: Jab application run hoti hai, ye method automatically execute hota hai.
- `new Person()`: Naya object banaate hain aur uska naam "John" set karte hain.
- `repository.save()`: Database mein save karte hain.
- `repository.findById()`: Us person ko id ke basis pe database se fetch karte hain.

✅ Pura ek chhota sa CRUD operation ka flow ready hai.

### 1.5 Important Points

- Repository ka implementation automatic hota hai: Tum sirf interface banao, class Spring khud banata hai.
- `@Autowired` ya `@Bean` ke andar injection automatic hota hai.
- CommandLineRunner ka use startup ke time pe koi kaam karne ke liye hota hai (jaise data insert karna).
- Optional handling karna important hai jab record fetch karte hain.

### 1.6 Extra Knowledge

Spring Data JPA mein different type ke repository interfaces available hain:

| Interface Name     | Kaam                                                 |
| ------------------ | ---------------------------------------------------- |
| Repository         | Basic level operations                               |
| CrudRepository     | Basic CRUD operations (Create, Read, Update, Delete) |
| ListCrudRepository | CRUD + List based operations                         |
| JpaRepository      | CRUD + Pagination + Sorting (Advance Level)          |

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
