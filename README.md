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

## Sending and processing event

![Sending and processing event](sending-processing-event.png)

The screenshot above shows that the publisher and subscriber are successfully connected through RabbitMQ. The subscriber was run first so it could listen to the `user_created` queue. After that, the publisher was run and sent 5 `UserCreatedEventMessage` events to RabbitMQ.

The subscriber received and processed all 5 messages:

1. `2406365231-Amir`
2. `2406365231-Budi`
3. `2406365231-Cica`
4. `2406365231-Dira`
5. `2406365231-Emir`

This shows the event-driven architecture flow. The publisher does not directly call the subscriber. Instead, the publisher sends events to RabbitMQ as the message broker, and the subscriber receives the events from RabbitMQ.

## Monitoring chart based on publisher

![Monitoring chart based on publisher](monitoring-chart-publisher.png)

The screenshot above shows the RabbitMQ monitoring chart after running the publisher several times. Each time the publisher is executed, it sends 5 `UserCreatedEventMessage` events to RabbitMQ. Because the publisher was run multiple times in a short period, the message rates chart shows several spikes.

The queued messages count is 0 because the subscriber was already running and consuming the messages. This means the messages were successfully delivered from the publisher to RabbitMQ and then processed by the subscriber. The spike appears only temporarily because RabbitMQ receives the messages, then the subscriber consumes them quickly.