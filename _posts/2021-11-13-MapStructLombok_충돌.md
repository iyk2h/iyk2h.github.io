## 문제

mapstruct가 정상적으로 작동하지 않았으며, "cannot find symbol"오류 발생



## 충돌 원인

mapstruct를 호출하는 방식이 조금 달라서 Lombok과 충돌이 발생



## 해결 방안

path 설정, 호출 순서는 mapstruct부터(gradle도 동일)



## 코드

``` xml
<!--Pom.xml-->

<properties>
  <java.version>11</java.version>
  <org.mapstruct.version>1.3.1.Final</org.mapstruct.version>
  <org.projectlombok.version>1.18.12</org.projectlombok.version>
</properties>
   
<dependencies>
  <dependency>
    <groupId>org.mapstruct</groupId>
    <artifactId>mapstruct</artifactId>
    <version>${org.mapstruct.version}</version>
  </dependency>
  <dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>${org.projectlombok.version}</version>
    <scope>provided</scope>
  </dependency>
  <!-- ... -->
</dependencies>

<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.5.1</version>
      <configuration>
        <!-- java 버전을 따름-->
        <source>11</source>
        <target>11</target>
        <annotationProcessorPaths>
          <!-- mapstruct 를 호출시 lombok 과 충돌 발생. 그래서 mapstruct와  lombok 에 대한 path 추가(mapstruct가 항상 lombok보다 우선 -->
          <path>
            <groupId>org.mapstruct</groupId>
            <artifactId>mapstruct-processor</artifactId>
            <version>${org.mapstruct.version}</version>
          </path>
          <path>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>${org.projectlombok.version}</version>
          </path>
        </annotationProcessorPaths>
        <compilerArgs>
          <!-- 아래와 같이 의존성을 추가하면 매번 mapper에 @Mapper(componentModel = "spring")를 지정하지 안아도 된다. -->
          <compilerArg>
            -Amapstruct.defaultComponentModel=spring
          </compilerArg>
        </compilerArgs>
      </configuration>
    </plugin>
  </plugin
</build>
	
```



### Reference

https://github.com/mapstruct/mapstruct-examples

["cannot find symbol"오류 git](https://github.com/mapstruct/mapstruct/issues/1270)