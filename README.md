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
19. countByLastname() method kis kaam mein aata hai?
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
