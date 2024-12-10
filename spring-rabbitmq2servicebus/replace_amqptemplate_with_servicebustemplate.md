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