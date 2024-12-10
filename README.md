## Convert Exception Handling from RabbitMQ to Azure Service Bus

To migrate exception handling from RabbitMQ to Azure Service Bus, perform the following steps:

1. Replace instances of `AmqpRejectAndDontRequeueException` with `ServiceBusException`.
2. When creating the new `ServiceBusException`, use `ServiceBusErrorSource.ABANDON` as the error source.
3. Ensure that `ServiceBusException` and `ServiceBusErrorSource` are properly imported from the Azure Service Bus library.

Example transformation:

```

// Before
throw new AmqpRejectAndDontRequeueException(e);

// After
throw new ServiceBusException(e, ServiceBusErrorSource.ABANDON);

```
## Convert Message Listener Annotation from RabbitMQ to Azure Service Bus

To migrate the message listener from RabbitMQ to Azure Service Bus, perform the following changes in your codebase:

1. Replace the `@RabbitListener` annotation with `@ServiceBusListener` annotation. This change updates the message listener to use Azure Service Bus instead of RabbitMQ.

2. Update the annotation parameter from `queues` to `destination` to align with Azure Service Bus configuration requirements.

Example transformation:

```

// Before
@RabbitListener(queues = "${rabitMq.dcs.queue.name}")

// After
@ServiceBusListener(destination = "${rabitMq.dcs.queue.name}")

```
## Integrate Azure Messaging Support via Annotation

To enable Azure messaging features in your application, add the `@EnableAzureMessaging` annotation to the relevant class. Ensure that the annotation is correctly imported from the Azure Spring Messaging library. This change will configure the class to support Azure messaging functionalities.

Example:

```

// Before
@Service

// After
@EnableAzureMessaging
@Service

```
## Import Required Classes for Message Construction

To enable the construction of messages with custom headers and content types, import the necessary classes from the Spring Messaging library. Specifically, add the following imports to your Java files:

```

// Before
// No imports for Message and MessageBuilder

// After
import org.springframework.messaging.Message;
import org.springframework.messaging.support.MessageBuilder;

```

These imports are essential for utilizing the `Message` and `MessageBuilder` classes in your code.
## Integrate Azure Dependency Management in Project

To integrate Azure dependency management into your project, you need to add a new `` section in your project's build configuration file. This section will manage Azure dependencies by importing the `spring-cloud-azure-dependencies` with a specified version. This ensures compatibility and helps manage transitive dependencies effectively.

Here is how you can implement this change:

1. Locate the build configuration file (e.g., `pom.xml` for Maven projects).
2. Add the following `` section if it does not already exist:

```

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.azure.spring</groupId>
            <artifactId>spring-cloud-azure-dependencies</artifactId>
            <version>5.17.1</version>
            <scope>import</scope>
            <type>pom</type>
        </dependency>
    </dependencies>
</dependencyManagement>

```

This addition will help manage Azure-related dependencies in a structured manner, ensuring that all Azure components used in the project are compatible with each other.
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
## Replace Messaging Template from AmqpTemplate to ServiceBusTemplate

To migrate from Spring RabbitMQ's `AmqpTemplate` to Azure Service Bus's `ServiceBusTemplate`, follow these steps:

1. **Import the Required Class:**
 - Replace the import statement for `AmqpTemplate` with `ServiceBusTemplate` from the Azure Spring Messaging library.
 
```

   // Before
   import org.springframework.amqp.core.AmqpTemplate;

   // After
   import com.azure.spring.messaging.servicebus.core.ServiceBusTemplate;
   

```

2. **Update Field Declaration:**
 - Change the field declaration from `AmqpTemplate` to `ServiceBusTemplate`.
 ```csharp
   // Before
   @Autowired
   private final AmqpTemplate amqpTemplate;

   // After
   @Autowired
   private final ServiceBusTemplate serviceBusTemplate;
   

```

3. **Modify Constructor:**
 - Update the constructor to accept `ServiceBusTemplate` instead of `AmqpTemplate`.
 ```csharp
   // Before
   public MessageController(AmqpTemplate amqpTemplate) {
       this.amqpTemplate = amqpTemplate;
   }

   // After
   public MessageController(ServiceBusTemplate serviceBusTemplate) {
       this.serviceBusTemplate = serviceBusTemplate;
   }
   

```

Ensure that all instances of `AmqpTemplate` in your code are replaced with `ServiceBusTemplate` to complete the migration.
## Construct and Send Message Using MessageBuilder and ServiceBusTemplate

To construct and send a message using `MessageBuilder` and `ServiceBusTemplate`, follow these steps:

1. Use `MessageBuilder` to create a message with the desired payload and custom headers.
2. Set necessary headers such as `customHeader` and `contentType` using the `setHeader` method.
3. Send the constructed message using the `serviceBusTemplate.send()` method.

Example transformation:
- Before:
 
```

  amqpTemplate.convertAndSend(DCSQueue, "", flareObject);
  

```

- After:
 ```csharp
  Message<FlareMessage> message = MessageBuilder.withPayload(flareObject)
      .setHeader("customHeader", "headerValue")
      .setHeader("contentType", "application/json")
      .build();
  serviceBusTemplate.send(DCSQueue, message);
  
```
## Convert Exception Handling to Use ServiceBusException

To align with Azure Service Bus standards, update the exception handling in your code by replacing `AmqpRejectAndDontRequeueException` with `ServiceBusException`. This change involves using `ServiceBusErrorSource.ABANDON` as the error source to indicate that the message should not be requeued. 

Example transformation:

```

// Before
throw new AmqpRejectAndDontRequeueException(e);

// After
throw new ServiceBusException(e, ServiceBusErrorSource.ABANDON);

```
