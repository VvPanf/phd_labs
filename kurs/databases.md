# Подключение баз данных

## MongoDB

docker-compose.yml
```yml
version: "3.7"

services:
  mongodb:
    image: mongo:latest
    container_name: mongodb
    ports:
      - "27017:27017"
```

Подключиться к консоли БД:
```bash
mongosh --port 27017
```

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

`application.properties`
```properties
spring.data.mongodb.host=localhost
spring.data.mongodb.port=27017
spring.data.mongodb.authentication-database=admin
spring.data.mongodb.username=root
spring.data.mongodb.password=example
spring.data.mongodb.database=books
spring.data.mongodb.auto-index-creation=true
logging.level.org.springframework.data.mongodb=DEBUG
```


## HSQL

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.hsqldb</groupId>
    <artifactId>hsqldb</artifactId>
    <version>2.7.1</version>
    <scope>runtime</scope>
</dependency>
```

`application.properties`
```properties
# Кофигурация самой базы данных
spring.datasource.url=jdbc:hsqldb:mem:database
spring.datasource.username=sa
spring.datasource.password=sa
spring.datasource.driverClassName=org.hsqldb.jdbc.JDBCDriver
# Конфигурация Spring Data
spring.jpa.database-platform=org.hibernate.dialect.HSQLDialect
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.jpa.hibernate.ddl-auto=create
```


## Redis

docker-compose.yml
```yml
version: "3.7"

services:
  redis:
    image: redis:latest
    container_name: redis
    ports:
      - "6379:6379"
    environment:
      - REDIS_PASSWORD=admin
```

Подключиться к консоли БД:
```bash
redis-cli
```

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

`application.properties`
```properties
spring.redis.database=0
spring.redis.host=localhost
spring.redis.port=6379
spring.redis.password=admin
spring.redis.timeout=60000
```


## SQLite

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.xerial</groupId>
    <artifactId>sqlite-jdbc</artifactId>
    <version>3.25.2</version>
</dependency>
```

`application.properties`
```properties
# Кофигурация самой базы данных
spring.datasource.url=jdbc:sqlite:sqlitesample:database
spring.datasource.username=admin
spring.datasource.password=admin
spring.datasource.driverClassName=org.sqlite.JDBC
# Конфигурация Spring Data
spring.jpa.database-platform=org.hibernate.dialect.HSQLDialect
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.jpa.hibernate.ddl-auto=create
```


## PostgreSQL

docker-compose.yml
```yml
version: "3.7"

services:
  postgres:
    image: postgres:latest
    container_name: postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_DB: "database"
      POSTGRES_USER: "admin"
      POSTGRES_PASSWORD: "admin"
```

Подключиться к консоли БД:
```bash
psql -U admin database

rem Чтобы показать все БД:
\l
```

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

`application.properties`
```properties
# Кофигурация самой базы данных
spring.datasource.url=jdbc:postgresql://localhost:5432/database
spring.datasource.username=admin
spring.datasource.password=admin
spring.datasource.driverClassName=org.postgresql.Driver
# Конфигурация Spring Data
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.jpa.hibernate.ddl-auto=create
```


## MySQL

docker-compose.yml
```yml
version: "3.7"

services:
  db:
    image: mysql:latest
    container_name: mysql
    ports:
      - "3306:3306"
    environment:
      - MYSQL_DATABASE=database
      - MYSQL_ROOT_PASSWORD=admin
```

Подключиться к консоли БД:
```bash
mysql -u root -p

rem Чтобы показать все БД:
show databases;
```

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency> 
    <groupId>mysql</groupId> 
    <artifactId>mysql-connector-java</artifactId> 
    <scope>runtime</scope> 
</dependency> 
```

`application.properties`
```properties
# Кофигурация самой базы данных
spring.datasource.url=jdbc:mysql://localhost:3306/database
spring.datasource.username=root
spring.datasource.password=admin
spring.datasource.driverClassName=com.mysql.jdbc.Driver
# Конфигурация Spring Data
spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.jpa.hibernate.ddl-auto=create
```


## Cassandra

docker-compose.yml
```yml
version: "3.7"

services:
  cassandra:
    image: cassandra:latest
    container_name: cassandra
    networks:
      - cassandra
    ports:
      - "9042:9042"
```

Подключиться к консоли БД:
```bash
cqlsh

rem Чтобы показать все БД:
describe keyspaces;
```

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-cassandra</artifactId>
</dependency>
```

`application.properties`
```properties
spring.data.cassandra.keyspace-name=database
spring.data.cassandra.contact-points=127.0.0.1
spring.data.cassandra.port=9042
```

[Подробнее можно посмотреть тут](https://www.bezkoder.com/spring-boot-cassandra-crud/)


## Elastic

docker-compose.yml
```yml
version: "3.7"

services:
  elasticsearch:
    image: elasticsearch:8.4.3
    container_name: elasticsearch
    environment:
      - node.name=elasticsearch
      - xpack.security.enabled=false
      - xpack.security.authc.api_key.enabled=false
      - discovery.type=single-node
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - "9200:9200"
      - "9300:9300"
  kibana:
    image: kibana:8.4.3
    container_name: kibana
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch
```

Подключиться к Elastic можно через Kibana. Там же можно посылать ему запросы.

Подключение БД к Spring:

`pom.xml`
```xml
 <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

[Подробнее можно посмотреть тут](https://howtodoinjava.com/spring-data/elasticsearch-with-spring-boot-data/)


## H2

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

`application.properties`
```properties
# Кофигурация самой базы данных
spring.datasource.url=jdbc:h2:mem:database
spring.datasource.username=sa
spring.datasource.password=sa
spring.datasource.driverClassName=org.h2.Driver
# Конфигурация Spring Data
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.jpa.hibernate.ddl-auto=create
```


## Clickhouse

docker-compose.yml
```yml
version: "3.7"

services:
  clickhouse-server:
    image: yandex/clickhouse-server
    container_name: clickhouse-server
    ports:
      - "8123:8123"
```

Подключиться к консоли БД:
```bash
clickhouse-client -m

rem Чтобы показать все БД:
show databases;
```

Подключение БД к Spring:

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>ru.yandex.clickhouse</groupId>
    <artifactId>clickhouse-jdbc</artifactId>
    <version>0.1.52</version>
</dependency>
```

`application.properties`
```properties
# Кофигурация самой базы данных
spring.datasource.url=jdbc:clickhouse://localhost:8123/database
spring.datasource.username=admin
spring.datasource.password=admin
spring.datasource.driverClassName=ru.yandex.clickhouse.ClickHouseDriver
# Конфигурация Spring Data
spring.jpa.database-platform=org.hibernate.dialect.Dialect
spring.jpa.generate-ddl=true
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.jpa.hibernate.ddl-auto=create
```