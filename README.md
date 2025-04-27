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
