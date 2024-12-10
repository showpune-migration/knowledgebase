## Remove Unnecessary Spring AMQP Dependency

To facilitate the migration from RabbitMQ to Azure Service Bus, remove the Spring AMQP dependency from the project. Specifically, delete the `spring-boot-starter-amqp` dependency from the `pom.xml` file, as it is no longer required.

Before:

```

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>

```

After:
The above dependency should be removed.