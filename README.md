# Publisher

## How much data does the publisher send to the message broker in one run?

In one run, the publisher sends 5 event messages to the message broker.

Each message is a `UserCreatedEventMessage` object that contains two fields:

- `user_id`
- `user_name`

The publisher sends these 5 messages by calling `publish_event()` five times. Each call publishes one `UserCreatedEventMessage` to the `user_created` queue through RabbitMQ.

So, in terms of the number of events, the publisher sends 5 events in one execution.

## The URL `amqp://guest:guest@localhost:5672` is the same as in the subscriber. What does it mean?

The publisher and subscriber use the same AMQP URL because both programs need to connect to the same RabbitMQ message broker.

In the URL:

```txt
amqp://guest:guest@localhost:5672

## Running RabbitMQ as message broker

![RabbitMQ running](rabbitmq-running.png)

The screenshot above shows that RabbitMQ is running successfully as the message broker. RabbitMQ provides the AMQP connection on port `5672`, which is used by the publisher and subscriber programs. It also provides the management dashboard on port `15672`, which can be opened in the browser to monitor connections, channels, exchanges, and queues.

In this tutorial, RabbitMQ acts as the middle component between the publisher and subscriber. The publisher sends events to RabbitMQ, and the subscriber listens to RabbitMQ to receive and process those events.