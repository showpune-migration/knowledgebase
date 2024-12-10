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