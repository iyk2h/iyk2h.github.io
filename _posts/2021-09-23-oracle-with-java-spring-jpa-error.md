### Registered driver with driverClassName=oracle.jdbc.driver.OracleDriver was not found, trying direct instantiation.

오라클 9 이후 oracle.jdbc.driver.OracleDriver 중단

application.properties 에서

`spring.datasource.driver-class-name=oracle.jdbc.driver.OracleDriver` -> `spring.datasource.driver-class-name=oracle.jdbc.OracleDriver`

