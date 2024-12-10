## Integrate Azure Service Bus with Spring Application

To integrate Azure Service Bus with your Spring application, add the following dependencies to your project's build configuration file (e.g., `pom.xml` for Maven projects):

1. Add the `spring-cloud-azure-starter` dependency to provide the basic setup for Azure services.
2. Add the `spring-messaging-azure-servicebus` dependency specifically for Azure Service Bus messaging.

Here is the XML snippet to include in your `pom.xml`:

```

<!-- Azure Service Bus dependencies -->
<dependency>
    <groupId>com.azure.spring</groupId>
    <artifactId>spring-cloud-azure-starter</artifactId>
</dependency>
<dependency>
    <groupId>com.azure.spring</groupId>
    <artifactId>spring-messaging-azure-servicebus</artifactId>
</dependency>

```

These additions will enable your application to communicate with Azure Service Bus, facilitating messaging capabilities.