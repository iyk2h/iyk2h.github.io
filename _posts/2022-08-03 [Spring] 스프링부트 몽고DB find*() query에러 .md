### spring boot with mongodb error

```
//error
at com.aks.springStorage.SpringStorageApplication.main(SpringStorageApplication.java:22) [classes/:na]
Caused by: org.springframework.data.mongodb.UncategorizedMongoDbException: Query failed with error code 2 and error message 'Field 'locale' is invalid in: { locale: "testDB" }' on server localhost:27017; nested exception is com.mongodb.MongoQueryException: Query failed with error code 2 and error message 'Field 'locale' is invalid in: { locale: "testDB" }' on server localhost:27017
```

```java
public interface CompanyRepository extends MongoRepository<Company, String> {
    List<Company> findByName(String name);

    @Query("{'id': ?0}")
    List<TestDB> findById(String id);
}

@Data
@Document(collation = "testDB") // 바로 이 부분이 이번 오류의 원인
public class TestDB {
    private int id;
    private String name;
    private String contact;
}
```

```java
@Data
@Document(collection = "testDB") // collation이 아닌 collection으로 적어야한다.
public class TestDB {
    private int id;
    private String name;
    private String contact;
}
```

