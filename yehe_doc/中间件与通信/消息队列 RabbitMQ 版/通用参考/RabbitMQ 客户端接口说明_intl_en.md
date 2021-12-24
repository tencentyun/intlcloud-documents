Below is the list of APIs supported by the RabbitMQ client:

| API | Description |
| ---------------------- | -------------------------------------------------------- |
| exchangeDeclare | Declares an exchange and creates one if it does not exist |
| exchangeDeclareNoWait | Declares an exchange and creates one asynchronously if it does not exist |
| exchangeDeclarePassive | Declares an exchange and reports an exception if it does not exist |
| exchangeDelete | Deletes an exchange |
| exchangeUnbindNoWait | Unbinds asynchronously |
| queueDeclare | Declares a queue and creates one if it does not exist |
| queueDeclareNoWait | Declares a queue and creates one asynchronously if it does not exist |
| queueDeclarePassive | Declares a queue and reports an exception if it does not exist |
| queueDelete | Deletes a queue |
| queueBind | Declares the binding between a queue and an exchange and binds them if they are not bound |
| queueBindNoWait | Declares the binding between a queue and an exchange and binds them asynchronously if they are not bound |
| queuePurge | Resets the consumption offset to consume from the latest message (i.e., deleting messages in native RabbitMQ) |
| queueUnbind | Unbinds |
| queueUnbindNoWait | Unbinds asynchronously |

