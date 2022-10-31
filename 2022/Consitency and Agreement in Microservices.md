# Consistency and Agreement in Microservices

Distributed transactions:

* MS DTC -> Two phase commit (aka 2PC):
  * Phase 1: Coordinator asking both resources to prepare for the transaction. Both resources give feedback about the transaction, it is still not commited.
  * Phase 2: Coordinator asking to commit the transaction.
* Not bullet-proof: A lot of network hops in between the phases.
* Works best with low latency :).
* Always on databases can't prepare the Phase 1
* Azure is also doesn't like that, but on IAS, you can manage the ports yourself.
* Same for NoSQL databases.
* Should also note that it takes around 10x longer then normal transactions.

Example:

* Consume AMQP
* Multiple writes to database
* Producing messages to AMQP
* All in a single "transactional" activity.

Epiphany:

* Assume a transactional boundary of a single aggregate.
* For example, rabbitMQ, one message
* At least one message, One processing.

Another example:

* Two aggregates with their own Business data.
* Adding Outboxes to both aggregates. Contains messages that needs to be send.
* Adding Inboxes to both aggregates. Contains messages already received.

Another another example:

* Three microservices with their own application and database.
* Using a *bus* that pulls messages from the outbox and putting it in the inbox.
* Business transaction with the database and adds the message to the outbox.
* With a Dispatcher (RabbitMQ), you'll send to the other microservice.
* If something goes wrong, the dispatcher will retry the message to the microservice.
* The retry will also try it on the microservice where it went correctly, but because the message is already in the inbox, it doesn't do anything anymore.
* The first microservice will remove the message when it's completed.

Sagas:

* Means of achieving distributed transaction.
* Series of event transactions, but also a series of compensating (most likely canceling) event transactions when failure occurs.
* All the transactions are standing on their own.
* It's far to expensive to keep this all open.
