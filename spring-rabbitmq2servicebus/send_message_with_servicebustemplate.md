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